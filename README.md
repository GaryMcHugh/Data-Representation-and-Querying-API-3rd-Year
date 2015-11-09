# Galway City Car Parking Locations
## Data Representation and Querying Project 2015
### Gary Mc Hugh

## Introduction
This project provides the design and documentation for the dataset "Galway City Car Parking Locations" which is available at [data.gov.ie](http://data.gov.ie) . It will provide users with a simple and easy way of accessing the data contained in this dataset.

## About the data
This dataset was received in Comma Separated Values (CSV) format, and was downloaded from [Galway City Car Parking Locations](https://data.gov.ie/dataset/galway-city-car-parking-locations/resource/154ab6f1-fa1e-454a-915d-18c561b75614).

The CSV file contains 18 rows, the first being a header row with the names of each field.
There are twelve values on each line, which are as follows:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| X Coordinate  | Identifies the exact easterly location                      |
| Y Coordinate  | Identifies the exact northerly location                     |
| Object ID     | Unique identifier for each row                              |
| Name          | The place name of the car park                              |
| Type          | What kind of car park it is                                 |
| No_Spaces     | The number of spaces in the car park                        |
| Latitude      | Determines location of Car Park                             |
| Longitude     | Determines location of Car Park                             |
| East ITM      | Location using Irish Transverse Mercator coordinate system  |
| North ITM     | Location using Irish Transverse Mercator coordinate system  |
| East IG       | Location using Irish Grid Reference System                  |
| North IG      | Location using Irish Grid Reference System                  |

Note: The X and Y Coordinate system are out dated and we would suggest that you use one of the other more up to date location systems that are available in this API such as :Lat and Long, ITM or IG.

## List of car parks
You can get the details of a car park in Galway with the name, the type and the number of spaces it contains using the GET method at the following URL:
*http://galwaycarparks.ie/carpark/[name]*
where you replace [name] with the name of the car park. Where there is a space in the name an underscore (_) should replace it.
For example, the URL:
*http://galwaycarparks.ie/carpark/Eyre_Square_Centre*
will return the general details of the Eyre Square Center car park.
The data will be returned in JSON format, with the following properties:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Name          | The place name of the car park                              |
| Type          | What kind of car park it is                                 |
| No_Spaces     | The number of spaces in the car park                        |

An example of a response would be:
```JSON
[ {"Name": "Eyre Sqaure Center", 
   "Type": "Multistorey Carpark",
   "No_Spaces": "452"}]
```
