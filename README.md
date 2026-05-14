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

class Main {
    +main(String[] args)
}

class WeatherController {
    -WeatherFeeder feeder
    -WeatherEventPublisher publisher
    +execute()
}

class WeatherFeeder {
    <<interface>>
    +fetch()
}

class OpenMeteoFeeder {
    -BeachProvider beachProvider
    -OpenMeteoUrlBuilder urlBuilder
    -OpenMeteoResponseParser parser
    -WeatherMapper mapper
    +fetch()
}

class BeachProvider {
    +getBeaches()
}

class WeatherEventPublisher {
    <<interface>>
    +publish()
}

class WeatherPublisher {
    -WeatherEventBuilder builder
    +publish()
}

class WeatherEventBuilder {
    +buildEvent()
}

class OpenMeteoUrlBuilder {
    +buildUrl()
}

class OpenMeteoResponseParser {
    +parse()
}

class WeatherMapper {
    +toWeatherRecord()
}

class WeatherRepository {
    <<interface>>
    +saveAll()
}

class SQLiteWeatherRepository {
    -WeatherDatabase database
    +saveAll()
}

class WeatherDatabase {
    +initialize()
    +connect()
}

class Beach {
    <<record>>
    +name
    +latitude
    +longitude
}

class WeatherRecord {
    <<record>>
    +beachName
    +forecastTime
    +temperature
    +windSpeed
    +capturedAt
}

Main --> WeatherController

WeatherController --> WeatherFeeder
WeatherController --> WeatherEventPublisher

OpenMeteoFeeder ..|> WeatherFeeder
WeatherPublisher ..|> WeatherEventPublisher
SQLiteWeatherRepository ..|> WeatherRepository

OpenMeteoFeeder --> BeachProvider
OpenMeteoFeeder --> OpenMeteoUrlBuilder
OpenMeteoFeeder --> OpenMeteoResponseParser
OpenMeteoFeeder --> WeatherMapper

OpenMeteoFeeder --> Beach
WeatherMapper --> WeatherRecord

SQLiteWeatherRepository --> WeatherDatabase
SQLiteWeatherRepository --> WeatherRecord

WeatherPublisher --> WeatherEventBuilder
WeatherEventBuilder --> WeatherRecord
```