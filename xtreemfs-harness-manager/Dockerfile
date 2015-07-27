FROM xtreemfs/xtreemfs-harness-common
MAINTAINER Christoph Kleineweber <kleineweber@zib.de>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qy install maven wget

RUN wget http://mirror.synyx.de/apache/tomcat/tomcat-6/v6.0.44/bin/apache-tomcat-6.0.44.tar.gz
RUN tar xvzf apache-tomcat-6.0.44.tar.gz
RUN sed -i 's/8080/30080/g' apache-tomcat-6.0.44/conf/server.xml

RUN git clone https://gitlab.harness-project.eu/chrkl/irm-xtreemfs.git && \
	cd irm-xtreemfs && \
	cd lib && \
	./add_to_local_maven_repo.sh && \
	cd .. && \
	mvn package && \
	rm -rf /apache-tomcat-6.0.44/webapps/ROOT && \
	cp target/ROOT.war /apache-tomcat-6.0.44/webapps/

RUN echo "#!/bin/bash" > /run_xtreemfs.sh
RUN echo "/usr/bin/java -ea -cp /xtreemfs/java/servers/dist/XtreemFS.jar:/xtreemfs/java/foundation/dist/Foundation.jar:/xtreemfs/java/flease/dist/Flease.jar:/xtreemfs/java/lib/* org.xtreemfs.dir.DIR /xtreemfs_data/dirconfig.properties &" >> /run_xtreemfs.sh
RUN echo "/usr/bin/java -ea -cp /xtreemfs/java/servers/dist/XtreemFS.jar:/xtreemfs/java/foundation/dist/Foundation.jar:/xtreemfs/java/flease/dist/Flease.jar:/xtreemfs/java/lib/* org.xtreemfs.mrc.MRC /xtreemfs_data/mrcconfig.properties &" >> /run_xtreemfs.sh
RUN echo "/usr/bin/java -ea -cp /xtreemfs/java/servers/dist/XtreemFS.jar:/xtreemfs/java/foundation/dist/Foundation.jar:/xtreemfs/java/flease/dist/Flease.jar:/xtreemfs/java/lib/* org.xtreemfs.scheduler.Scheduler /xtreemfs_data/schedulerconfig.properties &" >> /run_xtreemfs.sh
RUN echo "/apache-tomcat-6.0.44/bin/catalina.sh run" >> /run_xtreemfs.sh
RUN chmod +x /run_xtreemfs.sh

CMD [ "/run_xtreemfs.sh" ]
