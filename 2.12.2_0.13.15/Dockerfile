FROM openjdk:8
MAINTAINER aurel.paulovic

ENV	SCALA_VERSION="2.12.2" \
    	SBT_VERSION="0.13.15" \
	SCALA_HOME="/usr/local/bin/scala"

RUN	echo "####################################" && \
	echo 'Installing scala...' && \
	wget "https://downloads.lightbend.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz" && \
	tar xzf scala-$SCALA_VERSION.tgz -C /usr/local --strip-components=1 && \
	rm -rf scala-$SCALA_VERSION.tgz

RUN 	echo "####################################" && \
	echo 'Installing sbt...' && \
	wget "https://github.com/sbt/sbt/releases/download/v$SBT_VERSION/sbt-$SBT_VERSION.tgz" && \
	tar xzf sbt-$SBT_VERSION.tgz -C /usr/local --strip-components=1 && \
	rm -rf sbt-$SBT_VERSION.tgz

RUN	echo "####################################" && \
	echo 'Initializing sbt... this is going to take a lot of time and appear to be stuck, do not worry, that is just sbt and ivy being very slow' && \
	mkdir /tmp/dummy && \
	echo 'object TestApp { def main(args: Array[String]): Unit = println("Hello from Scala " + scala.util.Properties.versionNumberString)  }' > /tmp/dummy/TestApp.scala && \
	echo "scalaVersion := \"$SCALA_VERSION\"" > /tmp/dummy/build.sbt && \
	cd /tmp/dummy && \
	sbt -sbt-create run && \
	cd / && \
	rm -rf /tmp/dummy

RUN	mkdir /root/app

VOLUME /root/app

WORKDIR /root/app

CMD ["sbt", "-sbt-create"]
