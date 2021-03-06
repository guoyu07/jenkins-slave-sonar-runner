# Jenkins Slave Sonar Runner #

Jenkins Slave for Sonar Runner. Docker image based on OpenJDK official image.

	https://hub.docker.com/r/jnonino/jenkins-slave-sonar-runner/

## Docker Image Tags ##

-	[`jre-alpine` (*jre-alpine/Dockerfile*)](https://github.com/jnonino/jenkins-slave-sonar-runner/blob/master/jre-alpine/Dockerfile)
-	[`8-jre-alpine` (*8-jre-alpine/Dockerfile*)](https://github.com/jnonino/jenkins-slave-gradle/blob/master/8jre-alpine/Dockerfile)

## Tools Installed ##

- Sonar Runner
- Open Java JDK 8
- Git
- Subversion
- Mercurial
- wget
- curl
- unzip
- OpenSSH
- CA Certificates

## Add certificate to connect to HTTPS repositories

To add custom certificates and root CAs, create a new Dockerfile and import them with the following code.

	FROM jnonino/jenkins-slave-sonar-runner
	LABEL maintainer="Julian Nonino <noninojulian@outlook.com>"

	# Trust Root CA
	COPY Root_CA.crt /tmp
	RUN keytool -importcert -alias Root_CA -keystore ${JAVA_HOME}/jre/lib/security/cacerts -storepass changeit -file /tmp/Root_CA.crt -noprompt && \
		cp /tmp/Root_CA.crt /usr/local/share/ca-certificates/ && \
		chmod 644 /usr/local/share/ca-certificates/Root_CA.crt && \
		update-ca-certificates

	CMD ["/bin/bash"]
