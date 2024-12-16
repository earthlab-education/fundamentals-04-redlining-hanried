# **Redlining and Normalized Difference Vegetation Index (NDVI) in San Francisco, California**\

<figure>
    <img
        src="/notebooks/redlining-plots-images/san-francisco-holc-scan.jpg"
        alt="Redlining map of San Francisco, California. Mapping Inequality, public domain image."
        width="75%">
    <figcaption>Redlining map of San Francisco, California. Mapping Inequality, public domain image</figcaption>
</figure>

### Site Description:

San Francisco is a city in the Bay Area of California. It is located on the indigenous territories of the [Ohlone, Muwekma, and Ramaytush nations](https://native-land.ca/). The present-day [Muwekma Ohlone Tribe](https://www.muwekma.org/) includes all known surviving American Indian lineages native to the Bay Area.

Like many cities in the United States, San Francisco was subject to redlining by the federal government. A part of the federal government called the Home Owners’ Loan Corporation (HOLC) created Residential Security Maps between 1935 and 1940. These maps are also known as redlining maps and graded neighborhoods as an A, B, C, or D. Neighborhoods with an A grade, or “Best”, were colored green. B neighborhoods were “Still Desirable” and blue, C neighborhoods were “Definitely Declining” and yellow, and D neighborhoods were “Hazardous” and red. The redlining maps also included area descriptions for the neighborhoods, which included house and resident details, history of sales and rentals, descriptions of terrain, and favorable and detrimental influences. These area descriptions also included a trend of desirability. Mortgage companies saw neighborhoods with lower grades as riskier investments and were more likely to invest in higher grade neighborhoods. San Francisco’s Residential Security map was created in 1937.

In San Francisco’s pre-World War II real estate field, someone of Mexican, Central American, or South American heritage was considered white as long as they didn’t also have Native heritage. Additionally, Italian and Irish residents were considered white as well. Unfortunately, Asian residents were heavily discriminated against. This extended to San Francisco’s African American population as well.

The area descriptions of San Francisco’s redlining map focus on:
* the cost of buying or renting,
* physical features of the land,
* how the area is being maintained,
* the occupations of residents,
* the age and type of housing, and
* the types of businesses and community amenities present.
 
For example, in some A and B graded areas, it’s stated that there’s [“no threat of undesirable racial influences”](https://dsl.richmond.edu/panorama/redlining/map/CA/SanFrancisco/area_descriptions/B1#loc=13/37.7584/-122.4368) or [“no threat of racial concentration”](https://dsl.richmond.edu/panorama/redlining/map/CA/SanFrancisco/area_descriptions/B3#loc=13/37.7584/-122.4368). Conversely, in area [C4](https://dsl.richmond.edu/panorama/redlining/map/CA/SanFrancisco/area_descriptions/C4#loc=13/37.7497/-122.4373), it’s noted that “There are no racial concentrations in the area but there is a distinct threat of infiltration of Negroes and Japs from areas D-1 and D-3”. Area [B6](https://dsl.richmond.edu/panorama/redlining/map/CA/SanFrancisco/area_descriptions/B6#loc=13/37.7584/-122.4368), demonstrates the perceived importance of ownership, as it was “zoned second-residential but is 95% owner-occupied, which protects it from the infiltration of lower-class properties”. 

Citation:
Nelson, R. K., Winling, L, et al. (2023). Mapping Inequality: Redlining in New Deal America. Digital Scholarship Lab. https://dsl.richmond.edu/panorama/redlining.

### Data Description:
San Francisco's redlining data comes from the University of Richmond's third version of *Mapping Inequality: Redlining in New Deal America*. The scans of the redlining maps and area descriptions in the project are public domain. Specifically, the San Francisco map and area descriptions are from the [City Survey Files, 1935-1940](https://catalog.archives.gov/id/720357) at the National Archives. 

The multispectral data is accessed via earthaccess, ["a python library to search for, and download or stream NASA Earth science data with just a few lines of code"](https://earthaccess.readthedocs.io/en/latest/). Additionally, the [NASA Worldview Site](https://worldview.earthdata.nasa.gov/) was used to identify June 20, 2022, a clear day in San Francisco so that the multispectral data wouldn't have a lot of clouds. The reflectance data comes from the [Harmonized Landsat and Sentinel-2 (HLS) project](https://lpdaac.usgs.gov/documents/1698/HLS_User_Guide_V2.pdf?_gl=1*14eqerw*_ga*MTE0MDUzOTM2Ni4xNzMwOTQ2MzIy*_ga_PVF13VX9Z5*MTczMjc3NDE0MS42LjEuMTczMjc3NDYyNy4wLjAuMA..&_ga=2.231499167.1626254006.1732773970-1140539366.1730946322) from the "Operational Land Imager (OLI) and Multi-Spectral Instrument (MSI) onboard the Landsat-8 and Sentinel-2 remote sensing satellites respectively. The combined measurement enables global land observation every 2-3 days at moderate (30 m) spatial resolution."

### Methods Description:

After importing necessary packages and libraries and setting up a data directory, the redlining data for San Francisco, CA was downloaded. Then, two functions were defined. The first function processes the raster multispectral data file by opening and cropping the raster file. The second function applies the cloud mask to the multispectral data. Next, I used earthaccess to get the multispectral data for San Francisco, CA from June 20, 2022. After that, a regular expression was used to create a DataFrame with the raster multispectral metadata. For loops ran the newly created raster DataFrames through the two processing and cloud mask functions, yielding a dictionary with DataArrays of the blue, red, green, and NIR Narrow multispectral data. These band DataArrays were plotted to check for accuracy and then the red and NIR Narrow bands were used to calculate the Normalized Difference Vegetation Index (NDVI) DataArray. The NDVI DataArray was plotted with the San Francisco redlining data. Zonal Stats of NDVI were calculated for San Francisco's different neighboorhoods and a tree model was created with aforementioned zonal stats. 

See full code [here](https://hanried.github.io/earth_data_analytics_assignments/san-francisco-redlining-code.html).

### Plot 1:

<img
    src="/notebooks/redlining-plots-images/sf-ndvi-redlining-plot.png"
    width="50%">

**This plot shows a map of San Francisco, California showing the boundaries of the redlining zones from 1937 and the Normalized Difference Vegetation Index (NDVI) calculated from multispectral raster data captured via satellite on June 20, 2022.**
*A higher NDVI indicates healthier vegetation. The areas of high NDVI that stand out on the plot are in the northwest parts of San Francisco and are San Francisco's Golden Gate Park and Presidio (another large park). The high NDVI areas in the southwest corner of the plot are around Lake Merced and are three different Golf Courses. It is also important to note that the northwest corner of the plot, top edge of the plot, and east edge of the plot, are largely showing a very low NDVI because those areas are water. On land, the lowest levels of NDVI can be observed, generally, in the east side of San Francisco where there aren't any redlining boundaries. According to University of Richmond's context description of San Francisco's redlining, the "areas that were truly beyond the pale for residential mortgages were the areas that the HOLC did not survey at all, areas that might be described as "no-lined."" It could be interpreted then, that the "no-lined" areas of San Francisco have the lowest NDVI since they were not invested in by mortgage companies so it could have been more difficult to maintain those areas and keep healthy vegetation alive.*

### Plot 2:

<img
    src="/notebooks/redlining-plots-images/sf_redlining_ndvi_interactive_plot-static.png"
    width="15%">
*View the full interactive plot [here](file:///C:/Users/riede/Documents/Fall%202024%20Earth%20Data%20Analytics%20Class/Redlining%20Coding%20Challenge/notebooks/redlining-plots-images/sf_redlining_ndvi_interactive_plot.html).


<img
    src="/notebooks/redlining-plots-images/sf_redlining_ndvi_grade_means_df.png"
    width="15%">

**This plot includes two subplots: The first subplot on the left shows all of the grades of the redlined zones of San Francisco, CA. Zones with an "A" grade were considered the "Best" and are a dark teal color. Zones with a "D" grade were considered "Hazardous" and are a salmon color. The second subplot on the right shows the average NDVI for each redlined zone in San Francisco, CA. A higher NDVI value, which is a darker green color, indicates healthier vegetation. A lower NDVI value, which is a lighter green color, indicates less or unhealthy vegetation. The DataFrame below the subplots shows the mean NDVI grouped by neighborhood grade. For example, 0.324456 is the mean NDVI for all of the A graded neighborhoods.**

*Looking at these two subplots together, we can see that there is some relationship between the grade of the zone and NDVI. The darkest green and healthiest areas of vegetation are in A and B graded neighborhoods. All of the C and D graded areas have a paler green color on the NDVI plot. This indicates that there is some relationship between neighborhood grade and NDVI. One area of interest is around the Sutro Forest and Twin Peaks part of San Francisco, the large white spot in the middle of each subplot above. On the NDVI subplot, we can see that all neighborhoods around here have medium to dark green coloring, so healthier vegetation. Based on my analysis so far, that would indicate that the neighborhoods around the Sutro Forest/Twin Peaks area are A and B grades. However, out of the 13 neighborhoods that border Sutro Forest/Twin Peaks, 6 of them are A and B graded and 7 of them are C and D graded. Thus, I think these surrounding neighborhoods have higher NDVI mainly because they're surrounding a forested area, not because they're graded higher. Also, I wonder if some of the C and D graded areas on the east border of Sutro Forest/Twin Peaks would have been graded higher if there weren't no-lined and D graded areas farther to the east of them.*

*Looking at the subplots above and further plots below, it is important to take into account that some of the lowest areas of NDVI in Plot 1 on the east side of San Francisco were "no-lined" zones. So, since those zones weren't given a grade in San Francisco's redlining map, they aren't included in the subplots above or further plots below. This could affect our model later on.*

*Taking into account the DataFrame above that shows the total average NDVI for each graded area, we can see that as the grade decreases, so does the mean NDVI. This supports the idea that grade and NDVI are linked.*

### Plot 3:

<img
    src="/notebooks/redlining-plots-images/sf_redlining_tree_model.png"
    width="50%">

<img
    src="/notebooks/redlining-plots-images/sf_redlining_tree_model_errors.png"
    width="50%">

**The first figure above shows the tree model created to help determine if NDVI is related to redlining. The plot shows how accurate the tree model is by plotting the error of the tree model: the difference between the actual grade for each neighborhood and what the tree model predicts the grade to be based off the NDVI.**

*The tree model above was created with the individual mean NDVI for each neighborhood as the predictor values and the grade code for each neighborhood as the observed values. The model was created with a max depth of 2 and splits the data into 4 rectangles since we have 4 grade code categories. A tree model is helpful because it can work with numerical and categorical data, which is perfect as the grade codes are categorical and the mean NDVI is numerical. A downfall of the tree model is that it can be biased if the data it's trained on is unbalanced. In San Francisco's redlining map, there are 13 A graded neighborhoods, 35 B graded neighborhoods, 30 C graded neighborhoods, and 17 D graded neighborhoods. As these categories don't have super even numbers of neighborhoods, that could make the tree model less accurate.*

*Looking at the error plot, we can see that some neighborhoods, in yellow, were predicted incorrectly by 2 grades and some neighborhoods, in dark purple and green, were predicted incorrectly by 1 grade. The neighborhoods in blue were predicted correctly. Besides the yellow neighborhoods, there seems to be a pretty even mix of dark purple, blue, and green neighborhoods. So I think our tree model did an okay job of predicting the grade of a neighborhood based on NDVI. I think something else that could be hindering the tree model, besides the unbalanced categories, is the area around Sutro Forest/Twin Peaks. As discussed above, about 54% of the neighborhoods around Sutro Forest/Twin Peaks have a decent NDVI value but a C or D grade. If there was a perfect relationship between NDVI value and grade, those C and D neighborhoods would be graded higher because they have an NDVI similar to those of A and B grades. Finally, the fact that the "no-lined" zones on the east side of San Francisco aren't included in the tree model training data, could also have skewed our tree model into not seeing as big of a relationship between NDVI and grade.*

*In addition to the plots above, 3 cross-validation scores were calculated: 0.40625, 0.375, 0.32258065. Since our model has a max depth of 2 and four rectangles, any cross validation score over 0.25 supports the idea that NDVI and redlining grade are related. So these cross validation scores lightly support this relationship since they're above 0.25, but not by very much.*

### Conclusion:
In San Francisco, California, there is a slight relationship between NDVI value and the grade of a neighborhood. As the grade decreases from A to D, the total mean NDVI of those graded areas also decreases. The cross-validation scores of the tree model also support the relationship, although the scores aren't very high so the support is not very strong from the tree model. However, the tree model could have been skewed by the grades of the neighborhoods around Sutro Forest/Twin Peaks and the "no-lined" zones on the east side of San Francisco. These factors may have prevented the tree model from seeing a stronger relationship between NDVI and grade.