# GAM_models_temp_do
A series of scripts to isolate the interannual component of change in temperature and dissolved oxygen from environmental monitoring data

# Heading 1
### Data sources
estuary_shapefile_dictionary.csv = List of estuaries and associated shapefiles


# Scripts

### WIMS_data_cleaning_process_estuarine_samples.ipynb
Currently only set up for the format from WIMS.

To set up this script, place WIMS output data in the input_data folder of the estuary. A new folder will need to be set up for each estuary, and please use the name stored in the estuary_shapefile_dictionary.csv as your folder name.
The data used in this study can be sourced from the WQ archive (post 2000) or can be requested (pre 2000).

To run this script:
Ensure the estuary_shapefile_dictionary and WFD_shapefile are in place.
Run through cells.
Output cleaned csvs are stored in output_data/{estuary_name}
Output plots from the cleaning process are stored in output_data/{estuary_name}/cleaning_output_plots

The following output plots are generated:
A site map showing the samples spatially across an estuary coloured by distance to a the sea-estuary boundary
A before and after histogram of samples showing the sample depth screening process
A site map showing the before and after average salinity calculation
For each water quality parameter, a before and after filtering sample crossplot (with distance from sea boundary) is shown.

Known issues
--> Script currently only set up for WIMS data. needs to be amended for WQ archive
--> Mismatches with salinity mapping colour in plots


### 
*italic*
