# CS492 Project

Codes for data preprocessing and data abstraction for CS492 InfoVis course. 

In this project, we designed multiple views for MOOC users that help them to understand their and others' video navigation patterns better. We worked on MOOC sample data, which is private. 

Note: Proprocessing scripts in this folder can be very slow :) 

# Preprocessing - jsonize
  - Input: MOOC sample data files in 'MOOC_sample_data' folder (private).
  - Output: Json files in 'MOOC_sample_data_jsonized' folder, errorlist.csv
  1.  Transform raw data into json format. 
  2.  List ill-formatted events (mainly due to error occured in data extraction stage) in (file, line, raw event string) format in errorlist.csv. 

# Preprocessing - list_eventtypes
  - Input: MOOC sample data json files in 'MOOC_sample_data_jsonized' folder.
  - Output: A list of eventtypes in 'eventlist.csv'.
  - Note that you don't need this step if you already know which event types to analyze. 
  1.  List all eventtypes without duplications. 


# Filtering out - merge_videodata 
  - Input: MOOC sample data JSON files in 'MOOC_sample_data_jsonized' folder, list of target event types 'targetevent.csv' (in this project, video-related event types).
  - Output: A JSON file with all the target event data - 'videodata.json'
  1. Filter out events not related to the video navigation.
  2. Prettify video-related events by nesting "event" and "page" values, which are in string format.
  3. Save all the video-related events into 'videodata.json'.

# Filtering out - sessionwise_data 
  - Input: A JSON file with all the target event data - 'videodata.json', A csv file with a list of user id of interest 
  - Output: A csv file with a list of target video ids - 'targetvideos.csv', A JSON file with all the target video event data - 'video_targetdata.json', A JSON file with all the target video event but sorted for each session - 'video_targetdata_session.json', A JSON file with pause duration for pause events - 'video_targetdata_session_with_duration.json'.
  1. Get the list of video ids that the taget users have seen and save the list into 'targetvideos.csv'. 
  2. Filter out non-target video events and save the target video events data into 'video_targetdata.json'. Note this data contains non-target users' navigation histroy but only for the videos that the target users have seen. 
  3. Restructure the data into session-wise data where the events are sorted with the time (of event) and save it into 'video_targetdata_session.json'. 
  4. For pause events, calculate the pause duration. However, the pause events followed by stop (which means auto pause before stop event), we do not caclulated the pause duration. Save the data into 'video_targetdata_session_with_duration.json'. 
  
# Filtering out - sessionwise_nav_history 
  - Input: A csv file with a list of target video ids - 'targetvideos.csv', A JSON file with all the target video event but sorted for each session - 'video_targetdata_session.json', A JSON file with pause duration for pause events - 'video_targetdata_session_with_duration.json'.
  - Output: A JSON file with all the sessionwise video navigation history (playcount, speed for each 1 second grid points) - 'video_navhist_countspeed.json', A JSON file wit all the sessionwise video navigation history (playcount, speed for each 1 second grid points) and sum of pause duration for each 60 seconds grid point - 'video_navhist_countspeedpause.json'. 
  1. Calculate the max paly timestamp for each video. Here we assumed that the max timestamp is the latest timestamp that events of the video have. 
  2. Create empty grid to be used for navigation history. We made gridpoints for each 1 second. 
  3. Calculate navigatin count and speed for each timestamps and save the navigation history into 'video_navhist_countspeed.json'. 
  4. Calculate the sum of pause duration for each 60 seconds window and save it to each of the first grid points for each window. Save the navigatio history with pause duration data into 'video_navhist_countspeedpause.json'.
