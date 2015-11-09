# Galway City Car Parking Locations
## Data Representation and Querying Project 2015
### Gary Mc Hugh

## Introduction
This project provides the design and documentation for the dataset "Galway City Car Parking Locations" which is available at [data.gov.ie](http://data.gov.ie) . 

It will provide users with a simple and easy way of accessing the data contained in this dataset. This API has been designed to easily extract information on car parks in Galway with Tourists in mind. The API provides the name of all car parks in Galway city as well as data that can be inputed into sat nav's.

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
| Longitude     | Determines location of Car Park                             |
| Latitude      | Determines location of Car Park                             |
| East ITM      | Location using Irish Transverse Mercator coordinate system  |
| North ITM     | Location using Irish Transverse Mercator coordinate system  |
| East IG       | Location using Irish Grid Reference System                  |
| North IG      | Location using Irish Grid Reference System                  |

Note: The X and Y Coordinate system are out dated and we would suggest that you use one of the other more up to date location systems that are available in this API such as :Lat and Long, ITM or IG.

## List of car parks
Note: This function allows the user to get all the names of the Galway city car parks so they can be used in the other GET methods. This may be particulalry useful to tourists who do not know the name of the car parks.
You can get a list of all car park names in Galway city using the GET method at the following URL:
*http://galwaycarparks.ie/names*
This is a startic url, no fields of the url should to be changed.

For example, the URL:
*http://galwaycarparks.ie/names*
this will return all names of the car parks in Galway city.
The data will be returned in JSON format, with the following property:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Name          | The place name of the car park                              |

An example of a response would be:
```JSON
[ {"Name": "Eyre Sqaure Centre", 
   "Name": "Corrib Centre",
   "Name": "Market St"}]
```

## Details of a car park
You can get the details of a car park in Galway with the name, the type and the number of spaces it contains using the GET method at the following URL:
*http://galwaycarparks.ie/carpark/[name]*
where you replace [name] with the name of the car park. Where there is a space in the name an underscore (_) should replace it.
For example, the URL:
*http://galwaycarparks.ie/carpark/Eyre_Square_Centre*
will return the general details of the Eyre Square Centre car park.
The data will be returned in JSON format, with the following properties:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Name          | The place name of the car park                              |
| Type          | What kind of car park it is                                 |
| No_Spaces     | The number of spaces in the car park                        |

An example of a response would be:
```JSON
[ {"Name": "Eyre Sqaure Centre", 
   "Type": "Multistorey Carpark",
   "No_Spaces": "452"}]
```

## Longitude and Latitude
This function is designed to return the Longitude and Latitude of the car park so the user can input the result into a sat nav.
You can get the Longitude and Latitude of a car park using the GET method at the following URL:
*http://galwaycarparks.ie/satnav/[name]*
where you replace [name] with the name of the car park. Where there is a space in the name an underscore (_) should replace it.
For example, the URL:
*http://galwaycarparks.ie/satnav/Eyre_Square_Centre*
will return the Longitude and Latitude of the Eyre Square Centre car park.
The data will be returned in JSON format, with the following properties:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Longitude     | Determines location of Car Park                             |
| Latitude      | Determines location of Car Park                             |

An example of a response would be:
```JSON
[ {"Longitude": "-9.050422", 
   "Latitude": "53.272437",
   "No_Spaces": "452"}]
```
