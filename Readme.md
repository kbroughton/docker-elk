BigBrother

The purpose of this repo is to support logging and analytics on attacker side and server side machines.

All logs are ingested into elasticsearch. 
On the attacker side, we first focus on ingesting burp, cloudstrike and bash history.
The goal is to capture data from attacks for future analysis. Quality control and
The Logger++ extension for burp only supports Elasticsearch version 6.8 or less
and only unauthenticated connections. For this we use 


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
