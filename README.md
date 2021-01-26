# Data-Management-Lab
Final project of the course

Our project revolves around the transportation system in Dublin, Ireland.


1. In this reposity you will find a couple datasets:

        a. [stops.txt, stop_times.txt] - A set of datasets about the railway system in Dublin. That includes train stations, different rides, their respective schedules and the stops the different rides pass through.
  
        b. [hourly_Irish_weather.csv] - A dataset of Dublin hourly weather statistics in the years of 1990-2020. 
        
            The dataset is too large to upload quickly, so we attach the link to the kaggle site where the dataset could be found: 
            
            https://www.kaggle.com/conorrot/irish-weather-hourly-data
  
        c. [bicycle_2019.csv] - A dataset from 2019 which displays counters of the amount of bicycle riders that were spotted each hour, in varius locations in the city.
        
        d. [NTA_Public_Transport.csv] - A dataset that includes the correct ride times of the buses in Dublin
        
     
2. There is 1 .ipynb code file which contains both parts 1 and 2 of the project.
     
     The first cell in the notebook contains all the changable variables that the user can toy around with:
     
         a. kafka_server - the IP of the kafka server from whom the stream is drawn
         
         b. batch_path - the path of the batch file from whom the batch data is drawn
         
         c. model_path - the saving path of the ML model we used.
         
         d. src_loc, dest_loc - dictionaries that specify the latitude and longitude of the source geo-location of the user, and the desired destination geo-location
         
         e. user_timestamp - the time when the user wants to begin his trip
         
         f. WALKING_SPEED - the assumed walking speed of an average person
    
3. Project specification:

    Part A:
        
        In this part we repeat Tasks 2 and 3 from the assignments we received during the course. 
        
        This includes:
            
        a. Task 2:
            
            1. Imputing the 'vehicleSpeed' feature in various ways - mean imputation, pareto imputation and stochastic linear regression imputation.

            2. Training a Linear Regression model over features we select: 'currentHour', 'dateType', 'distanceCovered', 'vehicleSpeed', 'congestion', including the imputed 'vehicleSpeed'

            3. Performing predictions of the 'actualDelay' feature over the streamed data/batch data
                
        b. Task 3:
                
            4. Here we integrate two datasets into our original dataset: 'hourly_Irish_weather.csv' and 'bicycle_2019.csv'. After exploring and preprocessing them we add to our dataset the features 'avg_bicycle', 'rain', 'temp', which we also add to the set of features used in the training and prediction of our model.

            5. On this integrated dataset we again perform the imputation for the 'vehicleSpeed' feature and train a Linear Regression model to predict on the 'actualDelay' feature.
            
    Part B:
    
        In this part we devised an application which takes as input the source geo-location and the destination geo-location, and outputs two things:
        
            a. Best bus route:
            
                The source stop and the get-off stop which minimize the [ walking time to the stop + scheduled waiting time for the bus + predicted bus 'actualDelay' + ride duration + walking time to the destination ]
                
            b. Best train route:
            
                The source stop and the get-off stop which minimize the [ walking time to the stop + scheduled waiting time for the bus + ride duration + walking time to the destination ]
                
            Those outputs also include the walking time, the waiting time and the ride time.
            
            
We do note that the running time of our code isn't good enough for the purpose of choosing a ride in real time.

As a pointer for future work, we should index some information prior to running the live code to have a much faster response time.
