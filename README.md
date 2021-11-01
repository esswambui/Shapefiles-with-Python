# Shapefiles-with-Python
# Creating and Visualising Shapefiles using Python
### Libraries used:
- Geopandas
- Fiona
- Matplotlib
- Contextily
## Creating Shapefiles
### ShapefileGeneration.ipynb
I used the *fiona library* to create shapefiles from coordinates entered in
csv files. 
```python
pip install fiona
```
Each csv file *(provided in the geocordinates folder)* contains different types of coordinates i.e points, lines and polygons.
We read in each csv file using pandas
```python
import pandas as pd
pointDf = pd.read_csv('/content/cropPoints.csv',header=0)
```
Create a new shape file.
```python
pointShp = fiona.open('/content/cropPoints.shp', mode='w', driver='ESRI Shapefile',
          schema = schema, crs = "EPSG:4326")
```
Using fiona we store the coordinates (geometry) and properties into a dictionary and 
write the dictionary into the created file,
```python
for index, row in pointDf.iterrows():
    rowDict = {
        'geometry' : {'type':'Point',
                     'coordinates': (row.X,row.Y)},
        'properties': {'Name' : row.Name},
    }
    pointShp.write(rowDict)
#close fiona object
pointShp.close()
```
## Visualising the Shapefiles.
### kenyagpd.ipynb
Install geopandas 
```python
pip install geopandas
```
Read in the shapefiles *(provided in the **geokenya** folder)* using geopandas and
plot the geodataframe.            
Use contexily to plot a basemap that can be rendered on the web.
```python
import contextily as ctx
fig, ax = plt.subplots(figsize=(8,12))
ke_lines.plot(ax=ax, alpha=0.6)
ke_points.plot(ax=ax, alpha=0.6)
ctx.add_basemap(ax)
ax.axis('off')
```
**REMBER TO ADJUST THE FILE PATH ACCORDING TO YOUR SPECIFIC FILE NAME OR FOLDER YOU USE**
