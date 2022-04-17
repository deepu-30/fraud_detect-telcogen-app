# Detecting real time mobile-calls fraud with TelcoGenerator App

Services I used for this project is Windows VM > eventHubs > azure-stream-analytics > stroage 

Although this is my first project on github so I try my best to explain what I did in project...
With the help of Azure services I created a real time fraud detection in azure with the help of
TelcoGenerate app works on windows so for that I created a windows VM as I'm the user of ubuntu, then after creating vm I set up a remote desktop connection(RDP) then inside vm I install a zip file of TelcoGenereator app then unzip it and then next further process I will tell you through steps :

step 1 : After extraction go to the file telcodatagen.exe.config open that file with text editor there you see the coloumn of add key name and connection string we will get that using event hubs...
step 2 : I create a evenHub namespace called detect-events and in that I create event hub called input-events.

![Screenshot from 2022-04-17 19-43-00](https://user-images.githubusercontent.com/80934348/163718566-23b52c25-be3c-4252-b188-265c52e99c9c.png)

step 2 : click on input-events in that I create shared access policy and from that copy the connection string primary-key.

![Screenshot from 2022-04-17 20-03-15](https://user-images.githubusercontent.com/80934348/163719231-92afed82-68b8-4ebb-aa55-4658da74a1fe.png)

step 3 : add this connection string and eventhub name to telcodatagene.exe.conig by removing last entity-path including semicolon.

![Screenshot from 2022-04-17 19-32-41](https://user-images.githubusercontent.com/80934348/163719329-b9901823-6997-47fa-a5bf-15bd996f56c2.png)

step 4 : Now it's time to run the app, first copy the path for telcogenerator app then open cmd paste that path which looks like that..

![Screenshot from 2022-04-17 19-35-39](https://user-images.githubusercontent.com/80934348/163719455-44aa79c3-ea6f-4586-8a5f-5965d884823f.png)

step 5 : now finally run the app through the command which takes following parameter i.e, number of calls per hour, % of fraud probablitiy and the num of hours
cmd :   .\telcodatagen.exe 1000 0.2 2  
 
![Screenshot from 2022-04-17 19-36-28](https://user-images.githubusercontent.com/80934348/163719772-2a26ed41-f007-4086-bb4a-24927ea114ad.png)

step 6 : Now your app is running and sending data to eventhubs. Now it's time to create Stream Analytics job to process the event messages. I created the stream analytics naming > process-events-message.

step 7 : Here, we need two things in stream analytics first input via eventhubs and output via blobstorage though there are many other option for i/o services.
step 8 : click on add input and select event Hub it will automatically detect your eventHub name than create it..

![Screenshot from 2022-04-17 21-44-51](https://user-images.githubusercontent.com/80934348/163723134-909a9589-bdde-4916-95de-a48fa086fbd1.png)

step 9 : Now add output for that you have to create storage account in azure and add the container for saving the data coming from azure stream analytics and specify in stream analytics and it will detect the container name and select create...

storage-account with container
![Screenshot from 2022-04-17 21-07-11](https://user-images.githubusercontent.com/80934348/163722009-4de5d734-ca08-4197-8b3d-1e2c9ad9ffbe.png)

Adding output in stream-analytics
![Screenshot from 2022-04-17 21-44-24](https://user-images.githubusercontent.com/80934348/163723172-bfb9fc11-cbd5-4034-9d4f-e4e6ca676cbe.png)

step 10 : I have added I/O now for testing run the query..

![Screenshot from 2022-04-17 21-21-49](https://user-images.githubusercontent.com/80934348/163722193-57f065db-809f-44b7-875c-98ec4aa1ae58.png)

step 11 :  all works fine! then go to overview pane in stream analytics then click start for real-time processing messages and notice the graph....

![Screenshot from 2022-04-17 21-36-27](https://user-images.githubusercontent.com/80934348/163722814-7be261a8-2500-48d2-804d-408cea104f21.png)

step 12 : Now go to storage account and click on containers>date>[..] > there you see the output...

![Screenshot from 2022-04-17 21-33-48](https://user-images.githubusercontent.com/80934348/163722741-9e229c44-e51d-40f5-b1e1-0490ec84cff4.png)

And yeah that's it I created fraud detection on phone-calls through the Telcogenerator App.

I took a help from microsoft docs the link is given below :                                                                                                
     https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-real-time-fraud-detection



