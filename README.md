# Unit 10 Homework: Surf’s Up

## Location of folders

Part 1 code is in the jupyter notebook named "climate_starter.ipynb"
Part 2 code is in the python file named "app.py"

## Goal

 To help with your trip planning, you need to do some climate analysis on the area. The following sections outline the steps that I have taken to accomplish this task.

### Part 1: Climate Analysis and Exploration

In this section, you’ll use Python and SQLAlchemy to perform basic climate analysis and data exploration of your climate database. Complete the following tasks by using SQLAlchemy ORM queries, Pandas, and Matplotlib.

* Used the provided [starter notebook](climate_starter.ipynb) and [hawaii.sqlite](Resources/hawaii.sqlite) files to complete the climate analysis and data exploration.

* Used SQLAlchemy’s `create_engine` to connect to your SQLite database.

* Used SQLAlchemy’s `automap_base()` to reflect the tables into classes and saved a reference to those classes called `Station` and `Measurement`.

* Linked Python to the database by creating a SQLAlchemy session.

#### Precipitation Analysis

To perform an analysis of precipitation in the area, the following was done:

* Found the recent date in the dataset.

* Used this date to retrieve the previous 12 months of precipitation data by querying the 12 previous months of data.

* Selected only the `date` and `prcp` values.

* Loaded the query results into a Pandas DataFrame, and set the index to the date column.

* Sorted the DataFrame values by `date`.

* Plotted the results by using the DataFrame `plot` method, as shown in the following image:

  ![precipitation](Images/precipitation.png)

* Used Pandas to print the summary statistics for the precipitation data.

#### Station Analysis

To perform an analysis of stations in the area, the following was done:

* Designed a query to calculate the total number of stations in the dataset.

* Designed a query to find the most active stations (the stations with the most rows).

    * Listed the stations and observation counts in descending order.

    * Found the station ID with the highest number of observations.

    * Used the most active station ID, calculateed the lowest, highest, and average temperatures.

* Designed a query to retrieve the previous 12 months of temperature observation data (TOBS).

    * Filtered by the station with the highest number of observations.

    * Queried the previous 12 months of temperature observation data for this station.

    * Plotted the results as a histogram with `bins=12`

* Closeed the session.

- - -

### Part 2: Design the Climate App

A Flask API was designed based on the queries that were previously developed.

Flask was used to create the routes in the following manner:

* `/`

    * Homepage.

    * Listed all available routes.

* `/api/v1.0/precipitation`

    * Converted the query results to a dictionary using `date` as the key and `prcp` as the value.

    * Returned the JSON representation of your dictionary.

* `/api/v1.0/stations`

    * Returned a JSON list of stations from the dataset.

* `/api/v1.0/tobs`

    * Queried the dates and temperature observations of the most active station for the previous year of data.

    * Returned a JSON list of temperature observations (TOBS) for the previous year.

* `/api/v1.0/<start>` and `/api/v1.0/<start>/<end>`

    * Returned a JSON list of the minimum temperature, the average temperature, and the maximum temperature for a given start or start-end range.

    * When given the start only, calculated `TMIN`, `TAVG`, and `TMAX` for all dates greater than or equal to the start date.

    * When given the start and the end date, calculated the `TMIN`, `TAVG`, and `TMAX` for dates from the start date through the end date (inclusive).
