FROM base:ubuntu-12.10
MAINTAINER fwaibel@eclipsesource.com

RUN apt-get update
RUN apt-get install -y openjdk-7-jre-headless
RUN apt-get install -y curl
RUN apt-get install -y bsdtar

RUN useradd -m virgo

RUN curl -L 'http://download.eclipse.org/virgo/release/VP/3.6.2.RELEASE/virgo-tomcat-server-3.6.2.RELEASE.zip' | bsdtar --strip-components 1 -C /home/virgo -xzf -

# replace Spring 3.1.0.RELEASE with 3.2.5.RELEASE
RUN rm /home/virgo/repository/ext/org.springframework.*_3.1.0.RELEASE.*

RUN curl -L -o /home/virgo/repository/ext/org.springframework.spring-library-3.2.5.RELEASE.libd "http://ebr.springsource.com/repository/app/library/version/download?name=org.springframework.spring&version=3.2.5.RELEASE&type=library"

RUN curl -L -o /home/virgo/repository/ext/org.springframework.aop-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.aop&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.aspects-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.aspects&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.beans-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.beans&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.context-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.context&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.context.support-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.context.support&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.core-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.core&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.expression-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.expression&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.jdbc-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.jdbc&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.jms-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.jms&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.orm-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.orm&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.oxm-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.oxm&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.transaction-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.transaction&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.web-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.web&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.web.servlet-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.web.servlet&version=3.2.5.RELEASE&type=binary"
RUN curl -L -o /home/virgo/repository/ext/org.springframework.web.portlet-3.2.5.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=org.springframework.web.portlet&version=3.2.5.RELEASE&type=binary"

# replace AspectJ 1.6.12.RELEASE with 1.7.2.RELEASE
# remove old AspectJ 1.6.12.RELEASE
RUN rm /home/virgo/plugins/com.springsource.org.aspectj.weaver_1.6.12.RELEASE.jar
RUN rm /home/virgo/repository/ext/com.springsource.org.aspectj.weaver_1.6.12.RELEASE.jar

RUN curl -L -o /home/virgo/repository/ext/com.springsource.org.aspectj.weaver-1.7.2.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=com.springsource.org.aspectj.weaver&version=1.7.2.RELEASE&type=binary"
RUN curl -L -o /home/virgo/plugins/com.springsource.org.aspectj.weaver-1.7.2.RELEASE.jar "http://ebr.springsource.com/repository/app/bundle/version/download?name=com.springsource.org.aspectj.weaver&version=1.7.2.RELEASE&type=binary"

RUN sed -i -e 's/org.aspectj\.\*;version.*/org.aspectj.*;version="[1.7.2.RELEASE,2.0.0)",\\/' /home/virgo/configuration/org.eclipse.virgo.kernel.userregion.properties
RUN sed -i -e 's/^com.springsource.org.aspectj.weaver,.*/com.springsource.org.aspectj.weaver,1.7.2.RELEASE,plugins\/com.springsource.org.aspectj.weaver-1.7.2.RELEASE.jar,4,false/' /home/virgo/configuration/org.eclipse.equinox.simpleconfigurator/bundles.info

RUN chown -R virgo:virgo /home/virgo
RUN chmod u+x /home/virgo/bin/*.sh

ENTRYPOINT ["/home/virgo/bin/startup.sh"]
