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

## Class Diagram: weather-module

The following diagram illustrates the internal structure of the weather module:

```mermaid
classDiagram

%% ========= APP =========

class Main
class WeatherController

class WeatherFeeder {
  <<interface>>
  +fetch()
}

class OpenMeteoFeeder

class WeatherEventPublisher {
  <<interface>>
}

class WeatherPublisher


%% ========= INFRASTRUCTURE =========

class OpenMeteoUrlBuilder
class OpenMeteoResponseParser
class WeatherMapper

class WeatherRepository {
  <<interface>>
}

class SQLiteWeatherRepository
class WeatherDatabase


%% ========= MODEL =========

class Beach {
  <<record>>
}

class WeatherRecord {
  <<record>>
}


%% ========= RELATIONS =========

Main --> WeatherController

WeatherController --> WeatherFeeder
WeatherController --> WeatherEventPublisher

OpenMeteoFeeder ..|> WeatherFeeder
WeatherPublisher ..|> WeatherEventPublisher
SQLiteWeatherRepository ..|> WeatherRepository

OpenMeteoFeeder --> OpenMeteoUrlBuilder
OpenMeteoFeeder --> OpenMeteoResponseParser
OpenMeteoFeeder --> WeatherMapper

OpenMeteoFeeder --> Beach
WeatherMapper --> WeatherRecord

SQLiteWeatherRepository --> WeatherDatabase
SQLiteWeatherRepository --> WeatherRecord

WeatherPublisher --> WeatherRecord
```