FROM ubuntu

WORKDIR /Openfire
EXPOSE 5269
EXPOSE 5443
EXPOSE 5280
EXPOSE 5222
EXPOSE 9090

ENV DEBIAN_FRONTEND=noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN=true
ENV TZ=America/Los_Angeles
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get -yqq update \
&&  apt-get -yqq upgrade 
RUN apt install -yqq build-essential \
&&  apt install -yqq maven 
RUN DEBIAN_FRONTEND="noninteractive" apt install -yqq default-jre
RUN apt-get install -yqq git
RUN git clone https://github.com/igniterealtime/Openfire.git
RUN cd Openfire && make \
&& chmod +x mvnw \
&& ./mvnw verify 
RUN awk 'END{print $1}' /etc/hosts


ENTRYPOINT ["./Openfire/distribution/target/distribution-base/bin/openfire.sh"]



