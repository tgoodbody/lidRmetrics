# lidRmetrics
Additional point cloud metrics to use with *_metric functions in lidR. 


## Installation 

You can install the most recent version of the package by executing the code below:

```
install.packages("devtools")
devtools::install_github("ptompalski/lidRmetrics")
library(lidRmetrics)
```


## Example usage

All of the functions in lidRmetrics are designed to be used with one of the *_metrics functions in the lidR package (e.g. grid_metrics()). 

For example:

```
library(lidR)
library(lidRmetrics)

LASfile <- system.file("extdata", "Megaplot.laz", package="lidR")
las <- readLAS(LASfile, select = "*", filter = "-keep_random_fraction 0.5")

m1 <- cloud_metrics(las, ~metrics_basic(Z))

m2 <- grid_metrics(las, ~metrics_set1(Z), res = 20)

m3 <- grid_metrics(las, ~metrics_set2(X, Y, Z), res = 20)
```

## List of metrics




|                                    Metrics name                                    |                                                                                                                                                                                                                   Description                                                                                                                                                                                                                   |  metrics_* function   |                                                                                                                                             Notes                                                                                                                                              |
|:----------------------------------------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:---------------------:|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|
|                                         n                                          |                                                                                                                                                                                                             total number of returns                                                                                                                                                                                                             |     metrics_basic     |                                                                                                                                               NA                                                                                                                                               |
|                     zmax, zmin, zmean, zsd, zcv, zskew, zkurt                      |                                                                                                                                                                      elevation maximum, minimum, mean, standard deviation, coeficient of variation, skewness, and kurtosis                                                                                                                                                                      |     metrics_basic     |                                                                                                                                               NA                                                                                                                                               |
|                              zq1, zq5, …, zq95, zq99                               |                                                                                                                                                                                                              elevation percentiles                                                                                                                                                                                                              |  metrics_percentiles  |                                                                                                                                               NA                                                                                                                                               |
|                          pzabovemean, pzabove2, pzabove5                           |                                                                                                                                                          percentage of returns above a threshold. By default, percent of returns above mean elevation, above 2 and 5 m are calculated.                                                                                                                                                          |   metrics_percabove   |                                                                                                                                               NA                                                                                                                                               |
|                                        ziqr                                        |                                                                                                                                                                                                             interquartile distance                                                                                                                                                                                                              |  metrics_dispersion   |                                                                                                                                               NA                                                                                                                                               |
|                                zMADmean, zMADmedian                                |                                                                                                                                                                                           mean absolute deviation from the mean, and from the median                                                                                                                                                                                            |  metrics_dispersion   |                                                                                                                                               NA                                                                                                                                               |
|                                        CRR                                         |                                                                                                                                                                                                canopy relief ratio ((mean - min) / (max – min))                                                                                                                                                                                                 |  metrics_dispersion   |                                                                                                                                               NA                                                                                                                                               |
|                                   zentropy, VCI                                    |                                                                                                                                                                                          normalized Shanon diversity index, Vertical Complexity Index                                                                                                                                                                                           |  metrics_dispersion   |                                             van Ewijk, K. Y., Treitz, P. M., & Scott, N. A. (2011). Characterizing Forest Succession in Central Ontario using LAS-derived Indices. Photogrammetric Engineering and Remote Sensing, 77(3), 261-269                                              |
|                         zpcum1, zpcum2,..., zpcum8, zpcum9                         | canopy density metrics as defined by Woods et al 2008. Elevation range is divided into 10 equal intervals, and the cumulative proportion of returns in each interval is calculated. For example, zpcum3 is a cumulative percentage of returns located in lower 30% of maximum elevation. The results for the last (topmost) layer is not reported as it always equal to 100%. The number of layers (default = 10) can be specified by the user. | metrics_canopydensity |                                       M. Woods, K. Lim, and P. Treitz. Predicting forest stand variables from LiDAR data in the Great Lakes – St. Lawrence forest of Ontario. The Forestry Chronicle. 84(6): 827-839. https://doi.org/10.5558/tfc84827-6                                       |
|                       L1, L2, L3, L4, Lskew, Lkurt, Lcoefvar                       |                                                                                                                                                                          L-moments (L1, L2, L3, L4), L-moment skewness and kurtosis, L-moment coeficient of variation                                                                                                                                                                           |   metrics_Lmoments    |                                                                                                                                requires the {Lmoments} package                                                                                                                                 |
|                         lad_max, lad_mean, lad_cv, lad_min                         |                                                                                                                                                                                                     Metrics based on the leaf area density                                                                                                                                                                                                      |      metrics_lad      |                                                                                                                                               NA                                                                                                                                               |
| pz_below_0, pz_0.0.15, pz_0.15.2, pz_2.5, pz_5.10, pz_10.20, pz_20.30, pz_above_30 |                                                                                                                                                      Interval metrics - proportion of returns between specified elevation intervals. Default intervals are: 0, 0.15, 2, 5, 10, 20, and 30.                                                                                                                                                      |   metrics_interval    |                                                                                                                                               NA                                                                                                                                               |
|                                       rumple                                       |                                                                                                                                                                                                    A wrapper function for the rumple metric                                                                                                                                                                                                     |    metrics_rumple     |                                                                                                                                               NA                                                                                                                                               |
|                                         vn                                         |                                                                                                                                                                                                          total number of filled voxels                                                                                                                                                                                                          |    metrics_voxels     |                                                                                                                                               NA                                                                                                                                               |
|                                 vFRall, vFRcanopy,                                 |                                                                                                             filled ratio; FRall - a ratio between the number of filled voxels and all voxels located in the maximum extent of the point cloud. In case of  FRcanopy empty voxels above the canopy are excluded in the calculations                                                                                                              |    metrics_voxels     |                                                                                                                                               NA                                                                                                                                               |
|                                      vzrumple                                      |                                                                                                                                                                                                                 vertical rumple                                                                                                                                                                                                                 |    metrics_voxels     |                                                                                                                                               NA                                                                                                                                               |
|                                     vzsd, vzcv                                     |                                                                                                                                                                                         voxel elevation standard deviation and coeficient of variation                                                                                                                                                                                          |    metrics_voxels     |                                                                                                                                               NA                                                                                                                                               |
|                OpenGapSpace, ClosedGapSpace, Euphotic, Oligophotic                 |                                                                                                                                                                                                Canopy volume classes based on Lefsky et al 1999                                                                                                                                                                                                 |    metrics_voxels     | Lefsky, M. A., Cohen, W. B., Acker, S. A., Parker, G. G., Spies, T. A., & Harding, D. (1999). Lidar Remote Sensing of the Canopy Structure and Biophysical Properties of Douglas-Fir Western Hemlock Forests. Remote Sensing of Environment, 70(3), 339–361. doi:10.1016/S0034-4257(99)00052-8 |
|                  kde_peaks_count, kde_peaks_elev, kde_peaks_value                  |                                                                 Kernel density estimation applied to the distribution of point cloud elevation (Z). KDE allows to create a probability density function (using a Guassian kernel). The density function is then used to detect peaks (function maxima). Based on similar metric available in Fusion (see references), modified.                                                                 |      metrics_kde      |                                                                   McGaughey, R.J., 2021. FUSION/LDV: Software for LIDAR Data Analysis and Visualization. http://forsys.cfr.washington.edu/software/fusion/FUSION_manual.pdf                                                                    |
|                    pFirst pIntermediate pLast pSingle pMultiple                    |                                                                                                                                                                              Percentage of returns by echo types (First, Intermediate, Last; and Single, Multiple)                                                                                                                                                                              |     metrics_echo      |                                                                                                                                               NA                                                                                                                                               |
|                                        HOME                                        |                                                                                                                                                                                                             height of median energy                                                                                                                                                                                                             |     metrics_HOME      |                                                                                      calculations based on LAStools' implementation of the HOME metric. http://lastools.org/download/lascanopy_README.txt                                                                                      |

