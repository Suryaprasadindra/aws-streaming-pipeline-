# aws-streaming-pipeline-
this repo is creating pipeline for storing real time data.                                                 
Business - Problem :- 
our client is getting data in a real time, so he wants to store data and do analytics in real time.

solution : we gonna store real time data with the help of following AWS SERVICES - kinesis firehose,S3,kinesis analytical application(sql)
           creating 2 pipelines - 
             A. streaming------kinesis firehose data stream --------S3 ( it is just raw data )
	     B. streaming -----Kinesis firehose data stream --------analytics(sql)--------S3 ( it is semi processed data )

project  work-flow:-

1.First we are going to create s3 bucket in the name of S3RealTimeDataStorage
2.Next we are going to  create data stream ( kinesis data firehose ) :
                         source  -              DirectPut (where we are getting data in real time )
			 destination -           S3 ( we are using S3 service for storing data )
			 choose a bucket in S3 -  S3RealTimeDataStorage ( we created in the begining)
			 s3 bucket prefix -       realtimedata/  ( this realtimedata/folder will be created under S3RealTimeDataStorage & storing data under realtimedata folder)
			 s3 bucket error output prefix - error/  ( same as above but here error/ folder and stores errors if comes )
			 buffer size - 1 mb 
			 buffer interval - 60 seconds ( for every 60 seconds ,data is getting stored )
3. create another data stream for real time analytics applicatioon .
          same  steps as above
					 s3 bucket prefix -       analyticsdata/
			 s3 bucket error output prefix - analyticserror/  
					 
			 
4. test with demo data ( sending demo data to kinesis data firehose delivery stream ) :
          if you check realtimedata folder is s3 bucket , you can see data is storing in every 60 sec.

5. analytics applications :
       select sql applications (legacy) and create
			 provide  a name as dataanalytics
			 click on create legacy application
			 steps to configure you application 
			            configure source stream - 
				    source - kinesis data firehose delivery stream (mode of stream) and choose data stream ( new kinesis data stream )
				    schema - discover schema  ( automatically create schema based on data we are getting ) and save changes
				   real time analytics -  click on configure , you will get by default sql templates ( query for some specific tasks already saved ) and click on according to you analysis need. ( so analysis will happen in real time automatically )
				Destination - kinesis data firehose deliver system
				deliver stream -  B
				Output fomat - csv
				go to s3 bucket , you will find data under analyticsdata/ folder.
														
														
			 
     
   

