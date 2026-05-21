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
B -->|BeachInfo Events| MQ

MQ --> ES[eventstore-builder]
ES --> HIST[(Event Store)]

MQ --> BU[business-unit]

BU -->|updates beach state| DM[(Datamart)]
DM -->|provides BeachState| BU

BU -->|sends BeachState| REC[Recommendation Service]
REC --> OUT[Recommendations]
```