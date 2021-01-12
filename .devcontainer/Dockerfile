FROM ubuntu:20.04

ENV LANG en_US.UTF-8
ENV LC_ALL en_US.UTF-8
ENV LANGUAGE en_US:en

COPY *.crt /usr/local/share/ca-certificates/

RUN apt-get update \
  && apt-get install -qy gnupg ca-certificates \
  && update-ca-certificates \
  && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
  && apt-get install -qy curl \
  && curl https://download.mono-project.com/repo/xamarin.gpg | apt-key add - \
  && echo "deb https://download.mono-project.com/repo/ubuntu stable-focal main" >> /etc/apt/sources.list.d/mono-official-stable.list \
  && apt-get update \
  && DEBIAN_FRONTEND="noninteractive" apt-get -qy install tzdata \
  && apt-get install -qy mono-complete \
  && apt-get install -yq git automake autoconf libtool g++ coreutils policykit-1 \
        libgtk2.0-dev screen uml-utilities gtk-sharp2 python3 python3-pip \
  && rm -rf /var/lib/apt/lists/*

RUN curl -LO https://raw.githubusercontent.com/renode/renode/master/tools/requirements.txt \
  &&  pip3 install -r /requirements.txt \
  && pip3 cache purge \
  && rm /requirements.txt

WORKDIR /renode

#RUN git clone https://github.com/renode/renode.git
#RUN ./build.sh