# OpenSOC Vagrant

A collection of shell scripts and a Vagrant file for building an OpenSOC cluster. The goal of this project is to create be able to create a disposable OpenSOC cluster using Vagrant for development and testing purposes.

## Inspiration

Credit to https://github.com/vangj/vagrant-hadoop-2.4.1-spark-1.0.1 for the inspiration for this. This project is heavily influenced by that one.


## Running the clsuter

This project is meant to be as turn-key as possible. However, there are a couple things that need to be done besides running `vagrant up` before you can start using the cluster. At a high level they are:

* Place an RPM for Oracle's JVM in `resources/` and edit `common.sh` to set `JRE_RPM` to the name of the RPM
* Run `vagrant up`
* Format namenode for HDFS
* Start HDFS services

For convenience, this project ships with a fabfile that handles all of the setup tasks that must happen after running `vagrant up`. To run these tasks run the fabric task "postsetup" (`fab postsetup`)

## Caching Tarballs

The first time you run the script, a lot of very large tarballs need to be fetched. They will be cached to resources/tmp/ and the cached files will be used if you provision (`vagrant provision` or `vagrant destroy -f && vagrant up`) the VMs again.


## Virtual Machines

By default, 4 VMs will be created. They are named node1, node2, node3, and node4. Here is a breakdown of what services run where:

* node1
  * HDFS Namenode
  * Yarn Resourcemanager

* node2-4
  * Kafka Broker
  * Zookeeper
  * HDFS Datanode
  * YARN Nodemanager

## Port Forwarding

Some service's UIs are forwarded to localhost for ease of use. You can find the following services forwarded by default:

* HDFS - localhost:50070 -> node1:50070
* Storm UI - localhost:8080 -> node1:8080

## Progress

Here is a list of what will be provisioned via vagrant and its current status:

* Java - DONE
* Zookeeper - DONE
* HDFS/Yarn - DONE
* Kafka - DONE 
* Storm - DONE
* Hbase
* Hive
* Elasticsearch
* OpenSOC UI
* OpenSOC Storm Topologies

