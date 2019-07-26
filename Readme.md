# BigBrother

## Introduction

The purpose of this repo is to support logging and analytics on attacker side and server side machines.

All logs are ingested into elasticsearch. 
On the attacker side, we first focus on ingesting burp, cobaltstrike and bash history.
The goal is to capture data from attacks for future analysis. Quality control and
The Logger++ extension for burp only supports Elasticsearch version 6.8 or less
and only unauthenticated connections. For this we use 

A secondary goal is to add improved search capabilities to Burp.
For example, finding all unique values of a field in burp can be difficult, 
but this would be trivial in elasticsearch.

A simple python cli command or Kibana dashboard will be used to add context markers to elasticsearch.
Since engineers frequently switch campaigns, this will allow 
easily setting windows attack campaign annotations for us.

An example workflow would be:

Set the initial context for a new client
> bigbrother campaign config $PATH_TO_report.md

and then any time a new attack type is started
>bigbrother attack --attack-name authorization

Under the hood, this would post an entry to elasticsearch and all ingested data from 
that point to the next marker is considered part of the attack.

This makes supporting all tools and context switching easy.

## Getting Started

Install Docker and docker-compose (may come with osx install).

git clone https://github.com/kbroughton/docker-elk.git
cd elk6.8
docker-compose up

If you want to run in the background, run "docker-compose up -d"
Check the kibana and logstash at localhost:9200 and localhost:5601.

Install Logger++ Burp Extension.
The cluster name is docker-cluster. 
There is a 2 minute delay ingesting into elastic. You may want to decrease
this for testing.

In Kibana, use the [management tab](https://www.elastic.co/guide/en/kibana/current/index-patterns.html#settings-create-pattern)
to connect kibana to the elastic index named "logger".

Use the developer tools tab to run queries.

Use the machine learning tab to see top 10s of all fields
Machine Learning | Job Management | Create New Job | Data Visualizer

## Next steps:

Configure filebeat http://localhost:5601/app/kibana#/home/tutorial/systemLogs?_g=()
Support sync to authenticated elasticsearch in the cloud. Probably want to use elasticdump.
Add support for cobaldstrike.


## The Future

Elastic comes with SIEM, ML and Graph features.
It can ingest PaloAlto network format and parse logs from nearly any technology.

