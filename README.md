# installing scala for centos 7

Step 1: Update system
 $ sudo yum update -y && sudo reboot

Step 2: Install OpenJDK Environement
 $ sudo yum install java-1.8.0-openjdk.x86_64

validate Java runtime installation
  $ java -version

command should output:

openjdk version "1.8.0_262"
OpenJDK Runtime Environment (build 1.8.0_262-b10)
OpenJDK 64-Bit Server VM (build 25.262-b10, mixed mode)

Step 3: set the "JAVA_HOME" and "JRE_HOME" environment variables.

$ sudo cp /etc/profile /etc/profile_backup $ always backup your orig files
$ echo 'export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk' | sudo tee -a /etc/profile
$ echo 'export JRE_HOME=/usr/lib/jvm/jre' | sudo tee -a /etc/profile
$ source /etc/profile

validate your JAVA_HOME and JRE_HOME

$ echo $JAVA_HOME
$ echo $JRE_HOME

Step 4: Download and INstall Scala

$ cd ~
$ wget http://downloads.lightbend.com/scala/2.11.8/scala-2.11.8.rpm
$ sudo yum install scala-2.11.8.rpm

Verify your installtion

$ scala -version

Step 5: Run scala in interactive shell and or execute a function to quit :q

$ scala

scala> 1+2

scala> println("Hello Scala")

Step 6: Use scalac program to compile .scala source code.

$ vi hello.scala

object HelloWorld {
  def main(args: Array[String]) {
      println("Hello World!")
  }
}

$ scalac hello.scala
$ scala HelloWorld

Step 6: Embed Scala functions into a bash script, and then run the script using bash:

vi script.sh
Populate the file with:

#!/bin/sh
exec scala "$0" "$@"
!#
object HelloWorld extends App {
  println("Hello world!")
}

HelloWorld.main(args)

$ sh script.sh
