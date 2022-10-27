# AID-Project

## I - Developing the data warehouse

### 1. Creation of the airports database

Once connected to the MySQL server, we execute the command to create the provided airport database

`source airports.sql`

### 2. Creation of the airports data warehouse

We create 4 dimension tables and 1 fact table into the data warehouse airports_dw :
- dim_airline : Airline dimension
- dim_airplane : Airplane dimension
- dim_airport : Airport dimension for origin and destination
- dim_time : Time dimension for departure and arrival
- fact_flight : Fact table for flight

```
DROP DATABASE IF EXISTS airports_dw;

CREATE DATABASE airports_dw;

USE airports_dw;

CREATE TABLE dim_airline (
    AIRLINE_ID INT,
    AIRLINE_NAME VARCHAR(255),
    PRIMARY KEY (AIRLINE_ID)
);

CREATE TABLE dim_airplane (
    AIRPLANE_ID INT,
    AIRPLANE_TYPE VARCHAR(255),
    PRIMARY KEY (AIRPLANE_ID)
);

CREATE TABLE dim_airport(
    AIRPORT_ID INT,
    AIRPORT_NAME VARCHAR(255),
    CITY VARCHAR(255),
    COUNTRY VARCHAR(255),
    PRIMARY KEY (AIRPORT_ID)
);

CREATE TABLE dim_time(
    TIME_ID DATETIME,
    YEAR_ID INT,
    MONTH_ID INT,
    MONTH_NAME VARCHAR(255),
    DAY_ID INT,
    PRIMARY KEY (TIME_ID)
);

CREATE TABLE fact_flight(
    FLIGHT_ID INT,
    PASSENGERS_NUMBER INT,
    RECEIVE_TOTAL DOUBLE,
    AIRLINE_ID INT,
    AIRPLANE_ID INT,
    ORIGIN_AIRPORT_ID INT,
    DESTINATION_AIRPORT_ID INT,
    DEPARTURE_TIME_ID DATETIME,
    ARRIVAL_TIME_ID DATETIME,
    PRIMARY KEY (FLIGHT_ID),
    FOREIGN KEY (AIRLINE_ID) REFERENCES dim_airline (AIRLINE_ID),
    FOREIGN KEY (AIRPLANE_ID) REFERENCES dim_airplane (AIRPLANE_ID),
    FOREIGN KEY (ORIGIN_AIRPORT_ID) REFERENCES dim_airport (AIRPORT_ID),
    FOREIGN KEY (DESTINATION_AIRPORT_ID) REFERENCES dim_airport (AIRPORT_ID),
    FOREIGN KEY (DEPARTURE_TIME_ID) REFERENCES dim_time (TIME_ID),
    FOREIGN KEY (ARRIVAL_TIME_ID) REFERENCES dim_time (TIME_ID)
);
```
