+++
date = '2026-03-16T23:29:19+01:00'
draft = false
title = 'Minimum Viable Kubernetes'
+++

## Introduction 

The minimum circumstances where Kubernetes becomes a logical choice usually fall into three categories: Infrastructure Complexity, Operational Scale, and Business Requirements.


## Complexity Thresholds
If your "site" is a single monolith or just two containers (App + DB), Kubernetes is almost certainly overkill. 
It starts to make sense when you have many services that need to talk to each other, manage their own secrets, and scale independently. 
The manual effort of managing them on individual virtual machines (VMs) becomes higher than the effort of running K8s.

## Opertational Scale
Kubernetes is a bin-packer. Its job is to squeeze as many apps as possible onto the fewest number of servers to save money.

**High Variable Traffic**: If traffic spikes at 9:00 AM and drops at midnight, K8s Horizontal Pod Autoscaling (HPA) can automatically spin up replicas and shut them down.

**Multi/Hybrid Cloud**: Run the same environment on AWS, Google Cloud, and an on-premise server. Or taint towards a preference.

## Dedicated Expertise
Someone will need to be dedicated to maintaining one or more cluster/s. If automated testing and deployment pipelines is setup, K8s is a natural next step. 
If you are still manually SSH-ing into servers to pull code, K8s will likely make you pull your hair out.

## Budget
Monthly spend > $500 = K8s potential savings
