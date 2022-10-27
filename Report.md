# AID-Project

## I - Developing the data warehouse

### 1. Creation of the airports database

Once connected to the MySQL server, we execute the commands to create and go in the airports database.

`source airports.sql`

`use airports`

### 2. Creation of the airports data warehouse

We create 4 dimension tables and 1 fact table into the data warehouse airports_dw :
- dim_airline : Airline dimension
- dim_airplane : Airplane dimension
- dim_airport : Airport dimension for origin and destination
- dim_time : Time dimension for departure and arrival
- fact_flight : Fact table for flight


