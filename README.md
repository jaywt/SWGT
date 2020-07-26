# SWGT — Sliding Window Geospatial Tool
This is the revised __Python 3__ version of Sliding Window Geospatial Tool. The earlier version of SWGT is linked here: https://github.com/shawu810/RegionalCorrelation

## References
1. Li, Z., You, C., Gonzales, M., Wendt, A.K., Wu, F. and Brantley, S.L., 2016. Searching for anomalous methane in shallow groundwater near shale gas wells. _Journal of Contaminant Hydrology_, 195, pp.23-30. [Link to paper](https://doi.org/10.1016/j.jconhyd.2016.10.005)
2. Li, Z., You, C., Gonzales, M.S., Wendt, A.K., Wu, F. and Brantley, S.L., 2017. Corrigendum to “searching for anomalous methane in shallow groundwater near shale gas Wells”(J. Contam. Hydrol.(2016) 195 (23–30)(S0169772216300985)(10.1016/j. Jconhyd. 2016.10. 005)). _Journal of Contaminant Hydrology_, 207, pp.50-51. [Link to paper](https://doi.org/10.1016/j.jconhyd.2017.09.009)
3. Wen, T., Niu, X., Gonzales, M., Zheng, G., Li, Z. and Brantley, S.L., 2018. Big groundwater data sets reveal possible rare contamination amid otherwise improved water quality for some analytes in a region of Marcellus Shale development. _Environmental Science & Technology_, 52(12), pp.7149-7159. [Link to paper](https://doi.org/10.1021/acs.est.8b01123)

## Dependencies
This package was last tested on July 26, 2020. Testing environment is listed below:
| __Required Package__ | __Version__ |
|----------------------|-------------|
| Python               | __3.7.1__   |
| numpy                | 1.18.1      |
| pandas               | 1.0.0       |
| matplotlib           | 3.1.2       |
| scipy                | 1.3.1       |
| geopandas            | 0.6.1       |
| configparser         | 5.0.0       |


## How to run the code:
0. Make sure all of above dependencies are installed before running the code

1. Specify parameters in the configuration file, e.g., __example_config__.

2. Put your data under the directory specified in the configuration file (by input_path). The data should be a csv file with the following format:
```
# input csv files the columns should be:
# longitude, latitude, variable1, variable1 censor code, variable 2, variable 2 censor code
# all values need to be numerical.
# Censor code takes value from 0 or 1. 0 being uncensored value and 1 being left censored value (<).
# example:
#         -76.622689,41.94494,20.2,0,1795.712751,0
#         -76.622689,41.94494,20.2,0,1795.712751,0
#         -76.622689,41.94494,20.2,0,1795.712751,0
#         ...
```

3. Run the code
```bash
python main.py [your_config_file]
```
Alternatively, you can open the provided Jupyter Notebook __Sliding_Window_Geospatial_Tool.ipynb__ to run the first cell. This Jupyter Notebook also provides more advanced visualization options to produce publication-quality heatmaps.

4. Outputs are in the output folder. In the folder there are three files:
- [OUTPUT_PREFIX]_heatmap.pdf : The heatmap drawing.
- [OUTPUT_PREFIX]_corr_matrix.csv : The csv file for correlation matrix. Need to have this file for running the drawing code.
- [OUTPUT_PREFIX]_data_count_matrix.csv: The csv file for data matrix. Need to have this file for running the drawing code.
- [OUTPUT_PREFIX]_improved_heatmap.pdf : publication-quality heatmap.

### Only run drawing code:
Alternatively, you can only run the drawing code by:
```bash
python drawing.py [your_config_file]
```

## Example configuration file:
Here is a sample configuration file (sample.cfg).
```
[IO Parameter]
input_path = data/example_dataset_methane.csv
output_folder = output/
output_prefix = example

[Sliding Parameter]
step_size = 0.002
w_size = 0.05
measure = cenken
min_lng = -77
max_lng = -76
min_lat = 41.4
max_lat = 42.1
SKIP_THRES = 10

[Drawing Parameter]
tick_number = 10
tick_label_precision = 2
dpi = 500

[FLAGS]
NULL_FLAG = -10000000
```
