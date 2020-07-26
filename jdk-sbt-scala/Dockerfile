ARG SBT_VERSION=1.3.12
ARG SCALA_VERSION=2.13.2

FROM adoptopenjdk/jdk-11.0.8_10-alpine
ARG SBT_VERSION
ARG SCALA_VERSION

ENV SBT_VERSION=$SBT_VERSION
ENV SCALA_VERSION=$SCALA_VERSION

RUN apk add --no-cache --update wget libsodium-dev bash ca-certificates

RUN update-ca-certificates

RUN wget -qO - https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz > /tmp/sbt.tgz
RUN mkdir -pv "/usr/local/sbt"
RUN tar xzf /tmp/sbt.tgz -C "/usr/local/sbt" --strip-components=1
RUN ln -sv /usr/local/sbt/bin/sbt /usr/bin/
RUN sbt sbtVersion
RUN \
  mkdir -p project && \
  echo "scalaVersion := \"${SCALA_VERSION}\"" > build.sbt && \
  echo "sbt.version=${SBT_VERSION}" > project/build.properties && \
  echo "case object Temp" > Temp.scala && \
  sbt compile && \
  rm -r project && rm build.sbt && rm Temp.scala && rm -r target

WORKDIR /opt/workspace

RUN java -Xshare:dump

ENTRYPOINT ["sbt"]
