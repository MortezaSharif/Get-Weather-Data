# Get-Weather-Data
Access to weather data of each region using Python (Meteosatat library)
 # Import Meteostat library and dependencies

from datetime import datetime
import matplotlib.pyplot as plt
from meteostat import Point, Daily

# Set time period
start = datetime(2010, 1, 1)
end = datetime(2024, 5, 20)

# Create Point for Stuttgart,(Lon,Lat)%IR, ZAN,Ghazvin:50.53945526,36.02365296%
location = Point (35.68363290,51.39082601)

# Get daily data for 2023
data = Daily(location, start, end)
data = data.fetch()

# Plot line chart including average, minimum and maximum temperature
'''==['prcp']:mean monthly precipitation total in mm'''
'''==['wspd']:mean wind speed in km/h'''
'''==['pres']:mean sea-level air pressure in hPa'''


ax=data.plot(y=['tavg', 'tmin', 'tmax'])
ax.set_xlabel('Year')
ax.set_ylabel('Air Temperature (°C)')


plt.figtext(0.58, 0.89,'©2024 Linkedin:Morteza Sharif',size=8,weight='bold',color = '#797573')


plt.show()


#========================================
import time
print(time.ctime ())
start=time.time()
print('.................................')
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#*****Get area information using geolocation with Python*****

from datetime import datetime
from meteostat import Stations

stations = Stations()
stations = stations.nearby (35.68363290,51.39082601)#(31.00701745,48.25937164)
stations = stations.inventory('daily', datetime(2020, 1, 1))
station = stations.fetch(1)

print(station)
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#*****Get closest weather stations to Seattle, WA and convert distance to feet.*****

from meteostat import Stations, units

stations = Stations()
stations = stations.nearby (35.68363290,51.39082601)
stations = stations.convert({ 'distance': units.feet })
stations = stations.fetch(10)

print(stations)
#~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
#*****Get the number of weather stations in IRAN.*****

from meteostat import Stations

stations = Stations()
stations = stations.region('IR')

print('Stations in IRAN:', stations.count())



print('.................................')
print("Run Time:"+str(time.time()-start))
