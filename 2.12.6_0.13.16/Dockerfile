FROM openjdk:8
MAINTAINER aurel.paulovic

ENV	SCALA_VERSION="2.12.6" \
    	SBT_VERSION="0.13.16" \
	SCALA_HOME="/usr/local/bin/scala"

RUN	echo "####################################" && \
	echo 'Installing scala...' && \
	wget "https://downloads.lightbend.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz" && \
	tar xzf scala-$SCALA_VERSION.tgz -C /usr/local --strip-components=1 && \
	rm -rf scala-$SCALA_VERSION.tgz

RUN 	echo "####################################" && \
	echo 'Installing sbt...' && \
	apt-get update && \
	echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list && \
	apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823 && \
	apt-get install apt-transport-https && \
	apt-get update && \
	apt-get install sbt=$SBT_VERSION

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
