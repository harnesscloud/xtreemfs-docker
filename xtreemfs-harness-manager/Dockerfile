FROM xtreemfs/xtreemfs-harness-common
MAINTAINER Christoph Kleineweber <kleineweber@zib.de>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qy install maven wget

RUN wget http://mirror.netcologne.de/apache.org/tomcat/tomcat-6/v6.0.41/bin/apache-tomcat-6.0.41.tar.gz
RUN tar xvzf apache-tomcat-6.0.41.tar.gz

RUN git clone https://gitlab.harness-project.eu/chrkl/irm-xtreemfs.git && \
	cd irm-xtreemfs && \
	cd lib && \
	./add_to_local_maven_repo.sh && \
	cd .. && \
	mvn package && \
	rm -rf /apache-tomcat-6.0.41/webapps/ROOT && \
	cp target/ROOT.war /apache-tomcat-6.0.41/webapps/

CMD [ "/usr/bin/java","-ea","-cp","/xtreemfs/java/servers/dist/XtreemFS.jar:/xtreemfs/java/foundation/dist/Foundation.jar:/xtreemfs/java/flease/dist/Flease.jar:/xtreemfs/java/lib/*","org.xtreemfs.dir.DIR","/xtreemfs_data/dirconfig.properties","&&","/usr/bin/java","-ea","-cp","/xtreemfs/java/servers/dist/XtreemFS.jar:/xtreemfs/java/foundation/dist/Foundation.jar:/xtreemfs/java/flease/dist/Flease.jar:/xtreemfs/java/lib/*","org.xtreemfs.mrc.MRC","/xtreemfs_data/mrcconfig.properties","&&","/usr/bin/java","-ea","-cp","/xtreemfs/java/servers/dist/XtreemFS.jar:/xtreemfs/java/foundation/dist/Foundation.jar:/xtreemfs/java/flease/dist/Flease.jar:/xtreemfs/java/lib/*","org.xtreemfs.scheduler.Scheduler","/xtreemfs_data/schedulerconfig.properties","&&","/apache-tomcat-6.0.41/bin/startup.sh" ]

