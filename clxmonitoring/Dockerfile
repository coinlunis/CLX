FROM ubuntu:xenial
MAINTAINER LSH <55five@coinlunis.com>

ENV WS_SECRET peerpass
ENV PORT 3000

RUN apt-get update -y \
	&& apt-get -y upgrade \
	&& apt-get -o Dpkg::Options::=--force-confdef -y install curl netcat wget telnet vim bzip2 ssmtp locales python-pip software-properties-common python-software-properties bash-completion net-tools iputils-ping language-pack-ko \
	&& locale-gen ko_KR.utf8 \
	&& localedef -i ko_KR -c -f UTF-8 -A /usr/share/locale/locale.alias ko_KR.UTF-8 \
	&& chmod -R 777 /var/run /var/log /etc/passwd /etc/group \
	&& pip --no-cache install --upgrade pip 

RUN apt-get install -y tzdata \
	&& ln -sf /usr/share/zoneinfo/Asia/Seoul /etc/localtime \
	&& echo "Asia/Seoul" > /etc/timezone \
	&& dpkg-reconfigure -f noninteractive tzdata

ENV \
	LC_ALL=ko_KR.UTF-8 \
	LANG=ko_KR.UTF-8 \
	LANGUAGE=ko_KR.UTF-8

RUN apt-get update -y \
	&& apt-get install -y git \
	&& apt-get install -y sudo

RUN curl -sL https://deb.nodesource.com/setup_10.x | sudo bash - \
	&& sudo apt-get install -y nodejs

RUN git clone https://github.com/puppeth/eth-netstats.git

WORKDIR /eth-netstats

RUN npm install
RUN sudo npm install -g grunt-cli
RUN grunt

CMD npm start
