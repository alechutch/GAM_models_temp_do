# GAM_models_temp_do
A series of scripts to isolate the interannual component of change in temperature and dissolved oxygen from environmental monitoring data

# Set up
### Package install
Use the DO_temp_env.yml file to set up your environment.

You can do this with conda by using the following command:
conda env create --file DO_temp_env.yml

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


### MODEL_1_GAM_script_all_estuary_points_Model_1.ipynb
Reads in the cleaned csv data from the output_data/{estuary_name} folder

The following pieces of code can be changed:
1. the sampling window in the GAM function. This is the yearly interval the monte carlo calculation will extract the trend from.
2. The name of the yearly interval that is determined (note this does not change the yearly interval increments).
3. The determinand which is analysed. Must be spelt correctly.

This script will run, producing outputs for each estuary in the folder: output_data/{estuary_name}/MODEL_1_GAM_outputs_whole_estuary_{det}_1990_2022
The following plots are generated:
1. ActualVSPredicted_{estuary} - This provides a crossplot of the predicted vs actual measurements
2. Residuals_{estuary} - This provides a plot of the residuals from the model
3. Dependencies_{estuary} - This provides a graph of each of the partial dependencies in the model
4. Yearly_dependencies_{estuary} - This provides the graph of the partial dependency of float data, the trend used for this study
5. Random_model_posterior_sample_distribution_{estuary} - Random samples created from the posterior sample of the model
6. Random_yearly_dependence_posterior_sample_distribution_{estuary}
7. Monte_carlo_histogram_{estuary} - Histogram of trend built up from monte carlo simulations to provide average and standard deviation change over set time period

An individual csv is also deposited in the folder called "Humber_trend_result_list.csv" with the r^2 of the model, trend, stdeviation etc.

A combined results file is provided called: "Model_1_output_file_Temperature of Water_1990_2022.csv" which will store each of the individual estuaries datas in one file. hese are used for plotting.

### MODEL_2_GAM_script_all_estuary_points_sal_included.ipynb

This behaves the same way as model 1

### MODEL_3_GAM_script_all_estuary_points_Tensor.ipynb

This behaves similarly to model 1 and 2, with the notable differences:

1. An extra plot is produced: a 2D visualisation of day of year and float date (treated as a tensor).
2. The output files provide trends for each season

### MODEL_4_GAM_script_individual_sample_points.ipynb
The following pieces of code can be changed:
1. Either the yearly interval to sample over or the sampling window in the GAM function. Figures in the paper are reported with a 10 year interval.
2. The name of the yearly interval that is determined (note this does not change the yearly interval increments).
3. The determinand which is analysed. Must be spelt correctly.

Each of the plots in MODEL 1 are produced for each individual sample point.
In addition, a map is produced colour coded by the trend.
An individual output is set up for each 
