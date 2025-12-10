# AES509--Final-Project
Creating a module to extract HRRR data to create Convergence/Divergence, Vorticity, Temperature Advection, and Frontogenesis/Frontolysis plots.

For this project, I initially wanted to do something involving EFM data. Unfortunately, the code for EFM data was in binary and I have no experience using binary data. After taking an entire day trying to figure it out, I realized I didn't want to subject myself to that during finals week. So, I pivoted and looked for something where I can easily extract data since data extraction is a weakness of mine. AWS S3 Explorer (https://hrrrzarr.s3.amazonaws.com/index.html#sfc/), is something that we are actually using in AES 551 to extract data for our sea breeze project. I obviously wanted to do someting different from AES 551 so that I am not just copying. I initially wanted to look into snowstorms and analyze a specific snowstorm, but halfway through I realized I needed to just make a module that anyone can use for themselves. So, I created a module that extracts the HRRR data and returns 4 plots decided by the user. It's simple for a user, since they do not need to change anything except for the stuff under the if==main section at the end. This code was created by ChatGPT and Claude AI, after days of my input.    

A Walkthrough:
First, there are multiple import lines where the packages needed for the code are imported. Then, I have the one constant used in this module labeled as a constant by its ALL CAPS. 

1. HRRR Data Acess
def get_store is a function that accesses the HRRR model data and stores the data so the user doesn't have to download any files to their computer.
def get_grid is a function that retrieves a lat/lon grid from the website.
def load_h85 is a function that loads the 850 mb wind and temperature data from the website.
If the user wanted to change the level at which they are getting their data from, they would have to change this function.

2. Subsetting
def subset_box extracts a rectangular geographic region from our data (wind and temperature) around a latitude and longitude. It uses the half width that the user specifies in the if==main section, where the half width is the distance in degrees from the center point (basically how large the region is).

3. Diagnostics
This is where the equations for vorticity, convergence, temperature advection, and frontogenesis are generated. The user can use this section to add more code if they wanted to create more analysis plots.

4. Plotting (lat/lon axes, robust interpolation)
This section is where we create the plot of temperature and wind using the HRRR data. Bilinear interpolation is used in this section to smooth the contours for a nicer look. There is a also code that takes into account the NAN values. For a NAN value, it gets filled using its nearest point interpolation.
Temperature lines are also added in this section for a better analysis.
Lastly, lat/lon axes are created for the plots to get a better visualization of the region.


5. Main Worflow
Here, we have the code that creates the contour plots based on our diagnostic equations. Since in the if==main section the user decides which plots to be returned, we need code that can return or not return the plots.

6. If == Main
This is where the user can have freedom to analyze whichever day and diagnostic equation they want. The data goes back to August, 2016 up until this day.
The user can change the day, time in UTC, latitude and longitude, and half width.
They can also decide which plots get returned by using True/False, where using True returns the plot and using False doesn't return the plot. 



Lastly, I (AKA Claude AI) created fake data to use with my code in order to determine that my code is useful for data from somewhere else. My dummy test shows that my code isn't just an AI hallucination, rather it is actually using the data to create plots. 
