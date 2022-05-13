# 12 Factor App

A methodology for building cloud-native applications

https://12factor.net/


### Motivation

- to support modern application development
- to improve deployment portability
- to support the shift from hot deployment to continuous deployment and reduce turnaround cycle on deployments
- to support the shift from hosted/dedicated machines to cloud infrastructure

#### Goal

- scalability
- maintainability
- portability

#### Mechanisms

- immutability
- ephemerality
- declarative setups/configuration
- massive automation

#### The Principles

1. codebase
	- version control using code repositories - one repo per application
	- refrain from multiple application in the same repo
	- reasons:
		- to avoid entangling application history
		- to enable easy rollback of applications
		- to enable application decoupling
2. dependencies
	- should be explicitly declared and isolated
	- never rely on implicit existence of system-wide packages
    	- avoid checking in jar files
    	- avoid containers that provide implicit dependencies to an application eg runtime dependencies provided by application servers.
3. configuration
   - configuration externalisation
   - anything that changes between deployment environments should be strictly separated from the codebase.
   - reasons:
     - security
     - deployable artifact portability
4. backing services
   - should be treated as attachable resources
   - they should have a single entry point
   - they should be configurable for change
     - Example: datastores
5. build, release and run
    - a deployment process should be executable in 3 discrete steps
      - build to compile and generate artifacts
      - release to combine artifacts with configuration for a target environment
      - run to execute a release image that contains everything an application needs to run
6. processes
    - should be stateless
    - Eg avoiding sticky sessions
    - reasons:
      - to enable reliable elastic scaling without causing unpleasant application usage disruptions
7. port binding
    - in order to be self-contained, an application should not depend on external infrastructure for port binding and request handling
8. concurrency
    - scaling out by diversifying workload of processes
    - similar to the microservice architecture paradigm
9. disposability
    - an application should be quick to start up, graceful to shut down and resilient to failure
    - reasons:
      - Ease of replacement
      - Ease of adopting various deployment models
        - Rolling deployment
        - Blue-green release
        - Canary release
10. dev/prod parity
    - dev environment should be identical to production environment and every environment in between (staging)
    - reasons:
      - prevents introduction of bugs that would otherwise have been detected earlier
      - parity leads to reproducibility in any environment
11. logs
    - treat logs as event streams
    - applications should be agnostic to how logs are captured, processed and stored
    - reasons:
      - to enable elastic scalability of instances without concerns about storage
      - scoping applications to delivering its core business values
12. admin processes
      - processes such as database migration should be run in isolation
      - applies to tasks run by tools such as Flyway, Liquibase or scripted datastore operations.
      - reasons:
        - avoid disrupting or crashing production environments
