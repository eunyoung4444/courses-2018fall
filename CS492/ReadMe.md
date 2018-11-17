# CS492 Project

Codes for data preprocessing and data abstraction for CS492 InfoVis course. 

In this project, we designed multiple views for MOOC users that help them to understand their and others' video navigation patterns better. We worked on MOOC sample data, which is private. 

# Preprocessing - jsonize
  - Input: MOOC sample data files in 'MOOC_sample_data' folder (private).
  - Output: Json files in 'MOOC_sample_data_jsonized' folder, errorlist.csv
  1.  Transform raw data into json format. 
  2.  List ill-formatted events (mainly due to error occured in data extraction stage) in (file, line, raw event string) format in errorlist.csv. 

# Preprocessing - list_eventtypes
  - Input: MOOC sample data json files in 'MOOC_sample_data_jsonized' folder.
  - Output: A list of eventtypes in 'eventlist.csv'.
  1.  List all eventtypes without duplications. 


# Filtering out - merge_videodata 
  - Input: MOOC sample data JSON files in 'MOOC_sample_data_jsonized' folder, list of target event types (in this project, video-related event types).
  - Output: A JSON file with all the target event data - 'videodata.json', multiple JSON files (e.g., 'videodata_0,json') with target event data with smaller size (<128MB).
  1. Filter out events not related to the video navigation.
  2. Prettify video-related events by nesting "event" values, which are in string format.
  3. Save all the video-related events into 'videodata.json'.
  4. Save all the video-related events into multiple 'videodata_INT.json' files - so that Tableau can read each file. 

