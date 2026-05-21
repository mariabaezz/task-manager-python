# Task Manager in Python

Simple console task manager built with Python.

## Features
- Add tasks
- Show tasks
- Mark tasks as completed
- Delete tasks
- Delete all tasks
- Show summary
- Save tasks in JSON
- Prevent empty and duplicate tasks

## Technologies
- Python
- JSON
- Git

## How to run
```bash
python main.py
```

## Future improvements
Search tasks
Priorities
Tests

## System Architecture

```mermaid
flowchart LR

A[weather-module]
B[beachinfo-module]

A -->|Weather Events| MQ[ActiveMQ]
B -->|Beach Events| MQ

MQ --> ES[eventstore-builder]
MQ --> BU[business-unit]

ES --> HIST[(Event Store)]

HIST -->|Historical Events| BU

BU --> UPD[DatamartUpdater]
UPD --> DM[(Datamart)]

DM -->|BeachState| BU
BU -->|BeachState| REC[Recommendation Service]

REC --> OUT[Recommendations]
```