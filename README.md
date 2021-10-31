# Shapefiles-with-Python
# Creating and Visualising Shapefiles using Python
### Libraries used:
- Geopandas
- Fiona
- Matplotlib
- Contextily
## Creating Shapefiles
### ShapefileGeneration.ipynb
I used the *fiona library* to create shapes files from coordinates entered in
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
## Vusialising the Shapefiles.
