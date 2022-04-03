# NIFI-ELASTICSEACRH LIVE COIN TRACKING USING API
<p>  <br />
</p>
  
## Open Nifi WEBUI. 

### 1- Choose the "InvokeHTTP","JoltTransformJSON","PutElasticsearchHTTP" from the Add Processor Panel.
<img width="1124" alt="Ekran Resmi 2022-04-03 16 06 12" src="https://user-images.githubusercontent.com/91700155/161439644-d51533bd-12c6-4a6b-9048-ee0a85d5ae12.png">
<img width="826" alt="Ekran Resmi 2022-04-03 16 07 42" src="https://user-images.githubusercontent.com/91700155/161439692-e0233041-388b-4318-9b37-9267570d1577.png">

### 2- Configure "InvokeHTTP" processor.
<img width="784" alt="Ekran Resmi 2022-04-03 16 08 15" src="https://user-images.githubusercontent.com/91700155/161439775-14cd5da7-49a1-478a-b9b1-a830ab3cb003.png">

#### Include which site you want to extract data from.
##### For Example:
```console
https://api.btcturk.com/api/v2/ticker?pairSymbol=BTCUSDT
```
<img width="788" alt="Ekran Resmi 2022-04-03 16 10 09" src="https://user-images.githubusercontent.com/91700155/161439852-2aadd564-9470-47fd-b6c8-0bd0b6d281be.png">
 
 
### 3- Configure "JoltTransformJSON" processor.
<img width="775" alt="Ekran Resmi 2022-04-03 16 12 16" src="https://user-images.githubusercontent.com/91700155/161440033-3cc35772-1c32-49b8-9b03-54a13660b219.png">

##### For Example:

```console
[
    {
      "operation":  "shift",
     "spec":  {
       "data":  {
            "*":  {
      "pair": "pair",
      "pairNormalized": "pairNormalized",
      "timestamp": "timestamp",
      "last": "last",
      "high": "high",
      "low": "low",
      "bid": "bid",
      "ask": "ask",
      "open": "open",
      "volume": "volume",
      "average": "average",
      "daily": "daily",
      "dailyPercent": "dailyPercent",
      "denominatorSymbol": "denominatorSymbol",
      "numeratorSymbol": "numeratorSymbol",
      "order": "order"
	  }
   }
  }
 }
]
```
<img width="957" alt="Ekran Resmi 2022-04-03 16 12 33" src="https://user-images.githubusercontent.com/91700155/161440035-659b2714-52e8-4640-a3cb-863bd400d498.png">



### 4- Connect between the "InvokeHTTP" and "JoltTransformJSON"
<img width="744" alt="Ekran Resmi 2022-04-03 16 11 31" src="https://user-images.githubusercontent.com/91700155/161440123-bb58920d-8615-4db7-99bd-59e0b95dd6e1.png">


## Step first is done!
<img width="332" alt="Ekran Resmi 2022-04-03 16 11 41" src="https://user-images.githubusercontent.com/91700155/161440154-ba03a748-a1bb-490f-a8a1-4a8cb9cdd2d9.png">



### 5- Configure "PutElasticsearchHTTP" processor.
<img width="766" alt="Ekran Resmi 2022-04-03 16 18 42" src="https://user-images.githubusercontent.com/91700155/161440219-197763c4-48ee-488c-8be0-2098f308853c.png">

#### Include which your public IPV4 address you want to import data from.
##### For Example:
```console
http://ec2-52-29-193-171.eu-central-1.compute.amazonaws.com:9200
```
<img width="896" alt="Ekran Resmi 2022-04-03 16 19 29" src="https://user-images.githubusercontent.com/91700155/161440235-6ce30a66-d010-43cd-9c5d-db265f3d0d19.png">

#### Give a name with "-" that you use index for elastic and the type value is default "_doc".
<img width="772" alt="Ekran Resmi 2022-04-03 16 20 00" src="https://user-images.githubusercontent.com/91700155/161440307-3ccba0de-9c17-40d1-8a1f-12a5dd923a9c.png">
  

### 6- Connect between the "JoltTransformJSON" and "PutElasticsearchHTTP"
<img width="745" alt="Ekran Resmi 2022-04-03 16 13 09" src="https://user-images.githubusercontent.com/91700155/161440402-30f5476b-6a77-4c7b-8023-84df0373087c.png">

### 7- Create connection for the fail or retry situation.
<img width="740" alt="Ekran Resmi 2022-04-03 16 20 48" src="https://user-images.githubusercontent.com/91700155/161440482-9b0bdb9b-d5df-4d43-b61d-b8fd6e3e1df9.png">

 
## All steps are done!
<img width="555" alt="Ekran Resmi 2022-04-03 16 21 03" src="https://user-images.githubusercontent.com/91700155/161440521-f653fd8e-1657-4761-87d2-4e7b433b5db8.png">

 
 
## Open KIBANA WEBUI.  

 
### 1- Go to the "Management" panel. Choose the "Stack Management".

### 2- In the "Index Management" panel we will create template.
<img width="1422" alt="Ekran Resmi 2022-04-03 16 21 42" src="https://user-images.githubusercontent.com/91700155/161440672-cb2d269b-08bb-48f5-9975-457a113731be.png">

#### Write a value of your choice.
#### For the "Index Pattern" part, whatever you wrote in the "index" part in the Nifi "PutElasticsearchHTTP" field, you need to put "*" at the end here bc to pull all the data.
<img width="892" alt="Ekran Resmi 2022-04-03 16 22 46" src="https://user-images.githubusercontent.com/91700155/161440728-6250c259-d456-46dc-bcf1-eb2777060af5.png">

#### In the mapping part, we chose the "Date nanoseconds" field to observe the data per second. This part is not mandatory. If you don't want to edit or add anything, you can skip this field.
<img width="830" alt="Ekran Resmi 2022-04-03 16 25 08" src="https://user-images.githubusercontent.com/91700155/161440961-743a59e7-5c3a-436d-925a-c824f3e793fd.png">

#### The template has been created.
<img width="846" alt="Ekran Resmi 2022-04-03 16 25 20" src="https://user-images.githubusercontent.com/91700155/161440999-d697c517-467a-48b4-b244-ffc7ce99e015.png">

#### Now can see template in the Index Management Panel.
<img width="1431" alt="Ekran Resmi 2022-04-03 16 26 20" src="https://user-images.githubusercontent.com/91700155/161441042-43a23e46-fbd1-49ed-814e-9965ddbe7e63.png">


### 2- Go back to Nifi and run the all processors. 
<img width="369" alt="Ekran Resmi 2022-04-03 16 27 16" src="https://user-images.githubusercontent.com/91700155/161441081-6ae09efd-ea0a-4d22-af52-ec175756aa42.png">


### 3- On the other hand we can see the flowing data in the indices field under the index management panel after a few seconds.
<img width="1266" alt="Ekran Resmi 2022-04-03 16 27 40" src="https://user-images.githubusercontent.com/91700155/161441138-c72eda74-0c56-47e2-a2b2-da42d753b365.png">



 
### 4- In order for us to see the live data on our dashboard, we need to create an "Index Pattern" field.
#### Now go to Index Patterns" and then click the "Create Index Pattern".
<img width="1261" alt="Ekran Resmi 2022-04-03 16 28 10" src="https://user-images.githubusercontent.com/91700155/161441276-1c294db8-6f85-49f4-a78d-c70f77e6321f.png">

#### When I write "*" it will bring all the values of that data, the values entered with the same name will be matched in the side tab.
#### Here we must also select the timestamp' field that we edited earlier.
<img width="1063" alt="Ekran Resmi 2022-04-03 16 29 45" src="https://user-images.githubusercontent.com/91700155/161441360-9fdc3a82-7072-4e35-a56a-7440d7c9dce7.png">

#### The Create Index Pattern has been created.
<img width="1150" alt="Ekran Resmi 2022-04-03 16 29 55" src="https://user-images.githubusercontent.com/91700155/161441409-0fc7c7e1-fa3e-4b53-9d81-17c25e3097d3.png">

 
### 5- Now let's go to our dashboard.
#### I choose the metric type and choose my index pattern.
<img width="246" alt="Ekran Resmi 2022-04-03 16 31 16" src="https://user-images.githubusercontent.com/91700155/161441455-bff76d11-e364-4742-9271-973cba104530.png">
<img width="1410" alt="Ekran Resmi 2022-04-03 16 31 58" src="https://user-images.githubusercontent.com/91700155/161441608-f95e57a2-0b57-4b07-9d62-cf27fa9046f9.png">

 
#### I choose this because I want the data to refresh every 3 seconds. 
<img width="490" alt="Ekran Resmi 2022-04-03 16 32 38" src="https://user-images.githubusercontent.com/91700155/161441569-833fce2f-f066-4ebb-8205-b6b12b30aca4.png">

#### Now we can see the data streams changing every 3 seconds.
<img width="1413" alt="Ekran Resmi 2022-04-03 16 46 29" src="https://user-images.githubusercontent.com/91700155/161441665-42fa50e1-e571-452d-af91-03cb152930c0.png">

<img width="1423" alt="Ekran Resmi 2022-04-03 16 47 42" src="https://user-images.githubusercontent.com/91700155/161441671-30c43157-048a-4fc1-a3aa-4dc39c71d644.png">


<p>  <br />
</p>
<p>  <br />
</p>
Thank you :)


<p>  <br />
</p>

 ## Seda Atalay
