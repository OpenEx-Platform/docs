# OpenBAS Agent

## Introduction

The openBAS agent is an application whose main role is to enroll an asset on the OpenBAS platform,
to retrieve jobs or scripts to be executed and to transmit this information to the implants (subject to come)
for execution on the host asset.

The agent will not perform direct attack to remain neutral for antivirus.

It aims to be able to be run on different OS (Windows, Linux, macOS). It is developed in Rust

## Installation

Depending on the OS, several installations are at your disposal :

- Linux
  - Requirement → systemd, access to the openbas instance used
  - Installation → Create a service with name openbas-agent
  - Verification command line → `systemctl enable openbas-agent`
  - Start/Stop service →`systemctl start openbas-agent` & `systemctl stop openbas-agent`
- MacOS
  - Requirement → access to the openbas instance used
  - Installation → Create a service with name openbas-agent
  - Verification command line → `launchctl list | grep openbas.agent`
  - Start/Stop service → `launchctl bootstrap system ~/Library/LaunchDaemons/openbas-agent.plist` & `launchctl bootout system ~/Library/LaunchDaemons/openbas-agent.plist`
- Windows
  - Requirement → admin user, access to the openbas instance used
  - Installation → Create a service with name openbas-agent and
  - Verification command line → `Get-Service -Name "OBASAgentService"`
  - Start/Stop service → `Start-Service -Name "OBASAgentService"` & `Stop-Service -Name "OBASAgentService"`

The following flow diagram represents the Agent installation flow :

![img.png](assets/agent_installation_flow_diagram.png)

## Features

The main features of the OpenBAS agent are:
- Agent registration on the OpenBAS platform

  The agent is installed on the asset using an agent-installer.exe file and runs as a service.
  It communicates with the deployed OpenBAS instance in order to enroll the asset.

![Agent assets status](assets/agent_assets_status.png)

- Auto upgrade the agent (on start-up and registration)

- Retrieval of jobs to be executed

  The agent retrieves jobs to be executed from the OpenBAS instance every 30 seconds. 
  For the moment, jobs are implant launches on the asset to be able to execute attacks. 
  Each job execution logs is kept in a dedicated directory in order to have a trace of what happened (pid, executable).

- Deleting executables and execution directories

  The agent deletes implants that have been running for a predefined time and cleans the execution directories.

- Health check

  The agent pings the OpenBAS instance every 2 minutes to notify it of its healthy status.

- Cleanup

  The agent ensures that the processes it has executed are correctly finished or deleted if necessary. 
  The maximum time in minutes that a process associated with an execution directory can remain active is 20 minutes.

  The agent removes execution directories to avoid excessive disk space. 
  The maximum time in minutes that an execution directory can be kept before being deleted is 2 days.
