FROM centos:7.9.2009@sha256:be65f488b7764ad3638f236b7b515b3678369a5124c47b8d32916d6487418ea4
MAINTAINER GerritForge
# Allow remote connectivity and sudo
RUN yum -y install openssh-client initscripts sudo
# Add Gerrit packages repository
RUN rpm -i https://gerritforge.com/gerritforge-repo-1-2.noarch.rpm
# Install OpenJDK and Gerrit in two subsequent transactions
# (pre-trans Gerrit script needs to have access to the Java command)
RUN yum -y install java-1.7.0-openjdk
RUN yum -y install gerrit-2.13.1-1
USER gerrit
RUN java -jar /var/gerrit/bin/gerrit.war init --batch -d /var/gerrit
RUN java -jar /var/gerrit/bin/gerrit.war reindex -d /var/gerrit
# Allow incoming traffic
EXPOSE 29418 8080
# Start Gerrit
CMD /var/gerrit/bin/gerrit.sh start && tail -f /var/gerrit/logs/error_log
