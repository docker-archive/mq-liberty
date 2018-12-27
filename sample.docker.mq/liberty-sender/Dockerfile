FROM store/ibmcorp/websphere-liberty:webProfile8
USER root

MAINTAINER Dan Powers <dan.powers@docker.com>

COPY server.xml /opt/ibm/wlp/usr/servers/defaultServer/
COPY 9.1.1.0-IBM-MQ-Java-InstallRA.jar / 
COPY sender.war /opt/ibm/wlp/usr/servers/defaultServer/dropins/
	
RUN installUtility install --acceptLicense defaultServer
RUN java -jar 9.1.1.0-IBM-MQ-Java-InstallRA.jar --acceptLicense /

RUN mkdir -p /config/configDropins/overrides/ \ && echo '<server>\
<featureManager><feature>adminCenter-1.0</feature></featureManager>\
<quickStartSecurity userName="wsadmin" userPassword="wsadmin"></quickStartSecurity>\
<remoteFileAccess><writeDir>${server.config.dir}</writeDir></remoteFileAccess>\
</server>' > /config/configDropins/overrides/adminCenter.xml \ && installUtility install --acceptLicense defaultServer