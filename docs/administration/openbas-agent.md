# OpenBAS Agent

## Introduction

The openBAS agent is an application whose main role is to enroll an asset on the OpenBAS platform,
to retrieve jobs or scripts to be executed and to transmit this information to the implants (subject to come)
for execution on the host asset.

This application aims to be able to be run on different OS (Windows, Linux, macOS). It is developed in Rust

## Features

The main features of the OpenBAS agent are:
- Agent registration on the OpenBAS platform
  The agent is installed on the asset using an agent-instaler.exe file and runs as a service.
  It updates its status every 30 seconds on the OpenBAS platform.

- Auto upgrade the agent (on start-up and registration)

- Retrieval of jobs to be executed
  It retrieves the list of processes to be executed on the host asset,
  and created the implant to which it will transmit the scripts to be executed

- Deleting executables and execution directories
  The agent deletes implants that have been running for a predefined time and cleans the execution directories.

The following flow diagram represents the Agent installation flow :

![img.png](img.png)

