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
## Class Diagram: weather-module

The following diagram illustrates the internal structure of the weather module:

```mermaid
classDiagram

%% ================= APP =================

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
    +fetch() List~WeatherRecord~
}

class OpenMeteoFeeder {
    -BeachProvider beachProvider
    -OpenMeteoUrlBuilder urlBuilder
    -OpenMeteoResponseParser parser
    -WeatherMapper mapper
    +fetch() List~WeatherRecord~
}

class BeachProvider {
    +getBeaches() List~Beach~
}

class WeatherEventPublisher {
    <<interface>>
    +publish(WeatherRecord record)
}

class WeatherPublisher {
    -WeatherEventBuilder builder
    +publish(WeatherRecord record)
}

class WeatherEventBuilder {
    +buildEvent(WeatherRecord record) String
}


%% ================= INFRASTRUCTURE =================

class OpenMeteoUrlBuilder {
    +buildUrl(Beach beach) String
}

class OpenMeteoResponseParser {
    +parse(String json) Object
}

class WeatherMapper {
    +toWeatherRecord(Object data, Beach beach) WeatherRecord
}

class WeatherRepository {
    <<interface>>
    +saveAll(List~WeatherRecord~ records)
}

class SQLiteWeatherRepository {
    -WeatherDatabase database
    +saveAll(List~WeatherRecord~ records)
}

class WeatherDatabase {
    +initialize()
    +connect() Connection
}


%% ================= MODEL =================

class Beach {
    <<record>>
    +String name
    +double latitude
    +double longitude
}

class WeatherRecord {
    <<record>>
    +String beachName
    +String forecastTime
    +double temperature
    +double windSpeed
    +String capturedAt
}


%% ================= RELATIONS =================

Main --> WeatherController : starts

WeatherController --> WeatherFeeder : uses
WeatherController --> WeatherEventPublisher : publishes through

OpenMeteoFeeder ..|> WeatherFeeder
WeatherPublisher ..|> WeatherEventPublisher
SQLiteWeatherRepository ..|> WeatherRepository

OpenMeteoFeeder --> BeachProvider : uses
OpenMeteoFeeder --> OpenMeteoUrlBuilder : builds URLs
OpenMeteoFeeder --> OpenMeteoResponseParser : parses JSON
OpenMeteoFeeder --> WeatherMapper : maps data

OpenMeteoFeeder --> Beach : reads
WeatherMapper --> WeatherRecord : creates

SQLiteWeatherRepository --> WeatherDatabase : uses
SQLiteWeatherRepository --> WeatherRecord : stores

WeatherPublisher --> WeatherEventBuilder : uses
WeatherEventBuilder --> WeatherRecord : creates event from
```