# Galway City Car Parking Locations
## Data Representation and Querying Project 2015
### Gary Mc Hugh

## Introduction
This project provides the design and documentation for the dataset "Galway City Car Parking Locations" which is available at [data.gov.ie](http://data.gov.ie) . 

It will provide users with a simple and easy way of accessing the data contained in this dataset. This API has been designed to easily extract information on car parks in Galway with Tourists in mind. The API provides the name of all car parks in Galway city as well as data that can be inputted into sat nav's. A phone app could be designed to help tourists find car parks around Galway using this API.

## About the data
This dataset was received in Comma Separated Values (CSV) format, and was downloaded from [Galway City Car Parking Locations](https://data.gov.ie/dataset/galway-city-car-parking-locations/resource/154ab6f1-fa1e-454a-915d-18c561b75614).

The CSV file contains 18 rows, the first being a header row with the names of each field.
There are twelve values on each line, which are as follows:

| Field         | Description                                                 | Sample Data   |
| ------------- |:-----------------------------------------------------------:|:-------------:|
| X Coordinate  | Identifies the exact easterly location                      | -9.0535       |
| Y Coordinate  | Identifies the exact northerly location                     | 53.27308      |
| Object ID     | Unique identifier for each row                              | 1             |
| Name          | The place name of the car park                              | Market St     |
| Type          | What kind of car park it is                                 | Pay/Surface   |
| No_Spaces     | The number of spaces in the car park                        | 88            |
| Longitude     | Determines location of Car Park                             | 53.273        |
| Latitude      | Determines location of Car Park                             | -9.054        |
| East ITM      | Location using Irish Transverse Mercator coordinate system  | 529691.9      |
| North ITM     | Location using Irish Transverse Mercator coordinate system  | 725294.8      |
| East IG       | Location using Irish Grid Reference System                  | 129726.01     |
| North IG      | Location using Irish Grid Reference System                  | 225265.6      |

Note: The X and Y Coordinate system are a precise version of Longitude and Latitude.

## List of car parks
Note: This function allows the user to get all the names of the Galway city car parks so they can be used in the other GET methods below. This may be particularly useful to tourists who do not know the name of the car parks.

You can get a list of all car park names in Galway city using the GET method at the following URL:
*http://galwaycarparks.ie/names*

This is a static URL, no fields of the URL should to be changed.

For example, the URL:
*http://galwaycarparks.ie/names*
Will return all names of the car parks in Galway city.

The data will be returned in JSON format, with the following property:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Name          | The place name of the car park                              |

An example of a response would be:
```JSON
[ {"Name": "Eyre Square Centre", 
   "Name": "Corrib Centre",
   "Name": "Market St"}]
```

## Details of a car park
You can get the details of a car park in Galway with the name, the type and the number of spaces it contains using the GET method at the following URL:
*http://galwaycarparks.ie/carpark/[name]*

Where you replace [name] with the name of the car park. Where there is a space in the name an underscore (_) should replace it.

For example, the URL:
*http://galwaycarparks.ie/carpark/Eyre_Square_Centre*
Will return the general details of the Eyre Square Centre car park.

The data will be returned in JSON format, with the following properties:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Name          | The place name of the car park                              |
| Type          | What kind of car park it is                                 |
| No_Spaces     | The number of spaces in the car park                        |

An example of a response would be:
```JSON
[ {"Name": "Eyre Square Centre", 
   "Type": "Multistorey Carpark",
   "No_Spaces": "452"}]
```

## Longitude and Latitude
This function is designed to return the Longitude and Latitude of the car park so the user can input the result into a sat nav.
You can get the Longitude and Latitude of a car park using the GET method at the following URL:
*http://galwaycarparks.ie/satnav/[name]*

Where you replace [name] with the name of the car park. Where there is a space in the name an underscore (_) should replace it.

For example, the URL:
*http://galwaycarparks.ie/satnav/Eyre_Square_Centre*
Will return the Longitude and Latitude of the Eyre Square Centre car park.

The data will be returned in JSON format, with the following properties:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Longitude     | Determines location of Car Park                             |
| Latitude      | Determines location of Car Park                             |

An example of a response would be:
```JSON
[ {"Longitude": "-9.050422", 
   "Latitude": "53.272437"}]
```

## Car Park Type
This function is designed to return all car parks of the type inputted, this allows users to choose the type of car park they want to use.
You can get a list of names of the car parks of the type chosen by using the GET method at the following URL:
*http://galwaycarparks.ie/carpark/[type]*

Where you replace [type] with the type of the car park you want (multistorey or pay/surface).

For example, the URL:
*http://galwaycarparks.ie/carpark/multistorey*

Will return a list of car park names of type Multistorey.

The data will be returned in JSON format, with the following properties:

| Field         | Description                                                 |
| ------------- |:-----------------------------------------------------------:|
| Name          | The place name of the car park                              |
| Type          | What kind of car park it is                                 |

An example of a response would be:
```JSON
[ {"Name": "Eyre Square Centre", 
   "Type": "Multistorey Carpark",
   "Name": "Jurys Hotel", 
   "Type": "Multistorey Carpark"}]
```

## Adding a new car park
As Galway becomes larger more car parks will be required, or we may want to add car parks that surround Galway city. For this reason we need to be able to add more car parks to the dataset.

You can add a car park to the list of car parks in Galway city using the POST method at the following URL:
*http://galwaycarparks.ie/newcarpark*

This is an example of the message body that could be sent using the HTTP POST method to add data to this data set.
Note that the name/value pairs is sent in the HTTP POST request:

```HTTP
   POST /galwaycarpark/newcarpark HTTP/1.1
   User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
   Host: galwaycarparks.ie
   x="-9.0765"&y="53.2567"&objectid="18"&name="NewCarPark"&type="Multistorey"&no_space="555"&lat="53.225"&long="-9.087"&eastitm="529751.2"&northitm="725655.8"&eastig="129752.3"&northig="224866.5"
```

We use the POST method when we have data that we do not want everyone to see. The POST method offers a more secure way of adding data to our dataset like adding a new car park. If we were to use the GET method everyone could see the data that we are sending as it would be inside the URL. The post method is useful when we want to send sensitive data that we do not want everyone to see, like passwords or log in details.

## Deleting an existing car park
It is possible that a car park may need to be deleted from the dataset. This might be due to the car park closing and being replaced with a new building or if a mistake was made when adding the car park to the dataset.

The car park can be deleted from the dataset using the Object ID in the URL.

You can delete a car park from the list of car parks in Galway city using the DELETE method at the following URL:
*http://galwaycarparks.ie/delete/[ObjectID=?]*

Where you replace the question mark (?) with the ObjectID of the car park you want to delete. (See example below)

For example, the URL:
*http://galwaycarparks.ie/delete/ObjectID=2*

Will delete the car park with the Object ID of 2.

This is an example of the response you can expect from the DELETE method:

```HTTP
   HTTP/1.1 200 OK
   "Deletion was successful"
```

## Updating a car park
As Galway city grows they may need to add more car parking spaces to a car park. This could be achieved by adding a new floor to a multistorey car park or by a surface car park acquiring more space. For this reason we need to be able to update car parks

You can update a car park from the list of car parks in Galway city using the PUT method at the following URL:
*http://galwaycarparks.ie/update/[ObjectID]/[variable[?]]*

Where you replace:
1. The [ObjectID] with the object ID of the car park you want to update.
2. The [variable] with the name of the variable you want to update. 
3. The [?] with the new value of that variable.

For example, the URL:
*http://galwaycarparks.ie/update/2/No_Spaces402*

Will update the Jurys Hotel car parks number of spaces from 348 to 402.


This is an example of the http request that could be used:

```HTTP
   PUT /galwaycarpark/update/2/No_Spaces402 HTTP/1.1
   User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
   Host: galwaycarparks.ie
```

This is an example of the message body that could be sent back the HTTP PUT method for this data set.

```HTTP
HTTP/1.1 200 OK
Server: Server_Name
"Update was successful"
```
