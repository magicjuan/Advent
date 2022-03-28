FROM ubuntu:18.04 as advent-build
MAINTAINER  MagicJuan

##### Load requirements and perform builds

RUN apt-get update

RUN apt-get -y install make
RUN apt-get -y install gcc
RUN apt-get -y install gfortran

ENV TZ=GMT
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone
RUN apt-get -y install tzdata
RUN apt-get -y install texlive-binaries

RUN mkdir -p /usr/advent/src
WORKDIR /usr/advent/src

ADD builder/src.tgz .
ADD builder/Makefile .

RUN make depends
RUN make

FROM ubuntu:18.04 as advent-application

RUN apt-get update \
  &&  apt-get -y install libgfortran5 \
  &&	apt-get clean \
  &&	rm -rf /bd_build \
  &&	rm -rf /tmp/* /var/tmp/* \
  &&	rm -rf /var/lib/apt/lists/* \
  &&	rm -f /etc/ssh/ssh_host_*

RUN mkdir -p /usr/advent/bin
COPY --from=advent-build /usr/advent/src/bin /usr/advent/bin

WORKDIR /usr/advent/bin
ENV PATH=/usr/advent/bin:$PATH

CMD ["adv350"]
