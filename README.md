# IncrementalLoadADF

A basic example of incrementally loading relational data into Azure SQL database using Data Factory. Two Lookup activities look up old and new watermark values, which are connected by success to the copy data activity which does the incremental copy using this query on the source:

SELECT * FROM FactTrips WHERE 
LastModifiedTime > '@{activity('PreviousWaterMark').output.firstrow.WatermarkValue}'
AND
LastModifiedTime <= '@{activity('NewWaterMark').output.firstrow.WatermarkValue}';


Trigger1 is a schedule trigger that runs everyday. 

![image](https://user-images.githubusercontent.com/50174304/193459409-bf22a7e5-e276-4050-96c7-69dcc0df04b7.png)

