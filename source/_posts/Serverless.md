---
title: Serverless
toc: true
date: 2022-01-30 19:17:32
tags: 
- aws
- devops 
- cloud
categories: AWS
---



When the cloud is mentioned, its not only a server rental service. There is much more of it.\
Cloud is more about making your problem someone else's problem.\

Humanity has complex needs.\
Complex needs have complex solutions.\
Cloud services are used to decompose and abstract these complex solutions as much as possible.\
Since I think that devops has entered the side as serverless, I think every developer should improve themselves in this regard.\
Every developer should have something to tell to improve architecture design.\

I believe that learning cloud services will be help to think in that way.\
And one of the biggest cloud service provider is Amazon.\
I started learning AWS for that reason. AWS has roughly 150 services.\


## NON-CLOUD SOLUTION PROBLEMS 
Lets give an example with kafka, server and iot.

Let's say you have an online store.\
Your traffic will be shockingly high on black friday.\
With cloud services, you don't have to worry about it since it scales automatically.\

Partition numbers are set manually in Kafka.\
GlusterFS can fill up.\
Kafka can give errors.\


When these things happen, that evil thought comes to mind:\ 
<span style="color:red"><i>If only we used Monolithic architecture...</i></span>


SQS solves all these problems which are encountered using Kafka.\
Most importantly, monitoring can be done with SQS.\

Kibana needs to be installed in order to properly log real-time incoming data.\
But this can be done using AWS IOT Core and Kinesis.\

AWS does a good abstraction.\
Life getting more complex every second.\
We need abstraction in every field of it.\

