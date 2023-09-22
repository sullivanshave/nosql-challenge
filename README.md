# NoSQL Database (MongoDB)

## Introduction

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. I have been contracted by the editors of a food magazine, *Eat Safe, Love*, to evaluate some of the ratings data in order to help their journalists and food critics decide where to focus future articles.
## Data

The data is available from the [UK Food Standards Agency](https://ratings.food.gov.uk). The data is available in XML, CSV and JSON formats. I have chosen to use the JSON format.

## Methodology

1. Creating a MongoDB database called `uk_foods` and a collection called `establishments`.
1. Importing the data from the JSON file into the `establishments` collection via terminal.

    ```
    mongoimport --type json -d uk_food -c establishments_data --drop --jsonArray establishments.json
    ```
1. Using Python to query the database via the `PyMongo` library.
1. Add a restaurant that just opened to the database.

    ```
    {
        "BusinessName":"Penang Flavours",
        "BusinessType":"Restaurant/Cafe/Canteen",
        "BusinessTypeID":"",
        "AddressLine1":"Penang Flavours",
        "AddressLine2":"146A Plumstead Rd",
        "AddressLine3":"London",
        "AddressLine4":"",
        "PostCode":"SE18 7DY",
        "Phone":"",
        "LocalAuthorityCode":"511",
        "LocalAuthorityName":"Greenwich",
        "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
        "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
        "scores":{
            "Hygiene":"",
            "Structural":"",
            "ConfidenceInManagement":""
            },
        "SchemeType":"FHRS",
        "geocode":{
            "longitude":"0.08384000",
            "latitude":"51.49014200"
            },
        "RightToReply":"",
        "Distance":4623.9723280747176,
        "NewRatingPending":True
    }
    ```
1. Convert the `latitude` and `longitude` coordinates to decimal numbers and `RatingValue` to an integer.
1. Answer the following questions upon request of the magazine editors:
    * Which establishments have a hygiene score equal to 20?
    * Which establishments in London have a `RatingValue` greater than or equal to 4?
    * What are the top 5 establishments with a `RatingValue` of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
    * How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.


## Establishments in London that have a `RatingValue` Greater Than or Equal to 4

```
query = {"LocalAuthorityName": {"$regex": "London"}, 
          "RatingValue": {"$gte": 4}
          }

result = establishments.count_documents(query)

33 establishments have a `RatingValue` greater than or equal to 4 that are also in London.
```

## Top 10 Local Authority Areas in a Pandas DataFrame

| Area | Hygiene Score of 0 |
|-----|-------|
|Thanet|1130|
|Greenwich|882|
|Maidstone|713|
|Newham|711|
|Swale|686|
|Chelmsford|680|
|Medway|672|
|Bexley|607|
|Southend-On-Sea|586|
|Tendring|542|


# Further Findings can be found in the Jupyter Notebook files.