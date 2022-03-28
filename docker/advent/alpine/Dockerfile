FROM alpine:3.15.2 as advent-build
MAINTAINER  MagicJuan

##### Load requirements and perform builds
RUN apk add make
RUN apk add gcc
RUN apk add gfortran
RUN apk add texlive

RUN mkdir -p /usr/advent/src
WORKDIR /usr/advent/src

ADD builder/src.tgz .
ADD builder/Makefile .

RUN make depends
RUN make

FROM alpine:3.15.2 as advent-application

RUN apk add --no-cache libc6-compat
RUN apk add --no-cache libgfortran

RUN mkdir -p /usr/advent/bin
COPY --from=advent-build /usr/advent/src/bin /usr/advent/bin

WORKDIR /usr/advent/bin
ENV PATH=/usr/advent/bin:$PATH

CMD ["adv350"]
