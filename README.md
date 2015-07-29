# RasPy-Slideshow
##Random looping slideshow using Python, designed for Raspberry Pi implementation

This project was intially created for a loved one with Alzheimer's. The basic idea is to have a continually looping slideshow (similar to a digital picture frame) on a screen powered by Raspberry Pi. The slideshow
contains slides of various types, some static while others are drawn dynamically (i.e. date and weather) and others are dependent on the time of year.

If you are familiar with the disease, then you probably know that context is often a hard thing to come by. Faces don't always match up with names, "November" may not have any link to Thanksgiving, and so on. My goal here
was to provide context any day of the year through images, whether through the current weather (show a picture of rain instead of just saying "Rain"), upcoming holidays, seasons and linking faces to names. 

That being said, you could easily use this for your own RasPi purposes. I couldn't find anything else that was easy to "drag and drop" pictures into the different folders and just let it run. You could completely disregard any *slide type* that I used and come up with your own.

To see more about this project and how I built the display side please visit [Dynamic Alzheimer's Clock] (http://jpbrown.info/projects/view/dynamic-alzheimers-clock/) on my personal site.

**Requirements**
* tkinter
* httplib2
* PIL

##To Use
###Images
First, you need to decide how you want your image tree to be structured. I have provided my basic skeleton which contains a wide variety. You can add/remove as you like so long as you update **slideshow.py** in the relevant places.
* self.group_static (line 19) contains all of your slides that are eligible year-round, grouped by category
  * Each category contains a *name* and *method* ("image" or "draw", more on that later)
  * That category can include a number of slides which at a minimum have a *name* (not important) and *path* which points to the folder where your images are stored
  * Slides can provide a callback method if the *category method* is "draw", you must implement this method yourself elsewhere. See the 1st slide (Time of Day) for reference
* self.group_seasonal (line 51) contains all of your slides that you want to restrict by month
  * These function as other slides above, but with a *months* attribute that notes what number month the slide is eligible in

###Weather
If you want to use the weather capability you will need to update the zip code (and units if necessary) on line 86 as well as your own AppID (it's free)
```
self.weather_api_path = 'http://api.openweathermap.org/data/2.5/weather?zip=77034,us&units=imperial&APPID=bf21b5e020e1fcdbe8'
```
You could also implement more weather types and cloud types as you see fit. I kept it basic for now.


##Functionality
* F11 toggles fullscreen mode
* Escape key escapes fullscreen
* Transition time is set at 5 seconds, change this on line 192 `self.tk.after(5000, self.slideshow)` and remember to use miliseconds

##Other Notes
* Originally designed for a 1280x800 screen. This mostly matters for the static black image I use for Time of Day
* There are many quirks to getting PIL and tkinter to work on RasPi, especially with older distros. Leave a comment and I'll try to help

**Roadmap**
* Remote access/downloading of new slides
* Annual reminders (birthday, anniversary etc)
* Scheduled reminders i.e. "Haircut at 2PM"
