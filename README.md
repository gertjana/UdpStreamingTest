# Loraley

Test project that uses
 - Akka Http (UDP / HTTP connection)
 - Akka Reactive Streams (parse/transform udp packets)
 - Akka Actor
 - Hazelcast (store package information)
 
Actor Model

Uses hierarchical model 

for instance 2 packets with address 00:11:FF:AA and 00:22:FF:AA wil be stored like:

    RootActor
     \-> 0 (first char of address)
       \-> 0 (second char of address)
         |-> 1 (third char of address)
         |  \-> 1 (package 00:11:FF:AA will be stored here)
         \-> 2 (third char of second address
            \-> 2 (package 00:22:FF:AA will be stored here)
        

to start
 - optionally configure address/ports in application.conf
 - `sbt run` or
 - `sbt assembly` and then `java -jar target/scala_2.11/udp-streaming-test.jar`

run as a cluster
 - create multiple fat jars using `sbt assembly` with in each an unique application.conf
  - enable udp on only one
  - make sure http and hazelcast ports are unique 
  - start all with `java -jar name-of.jar`
 
