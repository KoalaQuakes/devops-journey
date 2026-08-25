+++
date = '2026-07-14T15:45:06+02:00'
draft = false
title = 'CI/CD Pipelines'
+++

**Beyond the "Pipeline" Metaphor**

## What is a pipeline
Continuous Integration and Continuous Delivery (CI/CD) are two halves of the software delivery process. However, referring to this process as a "pipeline" is an oversimplification, as there is rarely a single source or a fixed end point.

A more accurate comparison is global automotive manufacturing. Developers act as part suppliers, shipping individual components to a central facility where incoming packages are checked against quality and build specifications. This represents Continuous Integration (CI): developers commit code to a shared repository, which automatically triggers a battery of testing suites.

The second stage involves assembling, testing, and shipping the finished vehicles to customers at scale, accounting for various model customizations. This corresponds to Continuous Delivery (CD). The stakes are considerably higher here, as defects directly impact the end user. Continuous Delivery aggregates verified code into stable release candidates, which are then deployed via structured rollout strategies based on the organization's risk tolerance.


## The problem CI/CD solves
First, Continuous Integration (CI) provides a structured framework for tracking changes and aligning individual development progress toward a unified goal. It also reduces operational toil by automating repetitive, essential quality checks and compliance standards.

Second, Continuous Delivery (CD) eliminates the risks and high stress associated with large, infrequent deployments. It fundamentally transforms deployment cadence by replacing fire-fighting and reactive outage recovery with a predictable workflow. While the operational stakes remain high, CD normalizes release procedures throughout each sprint cycle.

**Key Operational Considerations**

Implementing CI/CD represents a significant operational shift that comes with distinct challenges—most notably, requiring total organizational commitment. To maintain pipeline integrity, all changes and emergency fixes must strictly adhere to the continuous integration process rather than bypassing it via ad-hoc adjustments.


## Relevant Tools
CI: Git / GitHub, Prettier, GitHub Code Scanning, Docker
CD/Observability: ArgoCD, OpenTelemetry, Grafana


## My Pipeline example
https://github.com/KoalaQuakes/ci-cd-pipe
