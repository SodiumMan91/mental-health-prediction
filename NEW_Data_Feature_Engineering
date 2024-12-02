# Datasets and Feature Engineering

This project used 3 datasets:

1. [CDC Places](https://www.cdc.gov/places/about/index.html): Contains census tract-level data regarding diseases and demographic 
2. [Smart Location](https://www.epa.gov/smartgrowth/smart-location-mapping#SLD): Contains census tract-level data regarding land use, transportation, and more
3. [New York Government Hospital Data](https://health.data.ny.gov/Health/Health-Facility-General-Information/vn5v-hh5r/about_data): Contains information about each hospital in New York

The CDC Places dataset and the SLD dataset were joined using GeoPandas. This was done by combining the region boundary column of the SLD dataset (a list of points making up the region boundary) and the lat/long points in the CDC dataset. This information suffices for GeoPandas to identify which CDC points fit within which SLD regions. The NY Hospital dataset was not explicitly joined to the remaining data but was instead used to create a new feature, "Distance to Nearest Hospital". Using the latitude and longitude for each hospital as well as the lat/long for each county, the Haversine formula was used to exhaustively find the nearest hospital to each county to populat the Distance to Nearest Hospital feature. 
