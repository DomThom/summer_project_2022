# Overview of folder

## Data in files
Real_data_ENSO.ipynb makes use of the Hadley SST dataset, which can be found here:
https://www.metoffice.gov.uk/hadobs/hadisst/data/download.html

Data used in smooth_comparison_data.ipynb is output from 949_ENSO_OH_yearly_alsoNOx.ipynb directly after computation of the eofs, so to recreate
the u-bl949 eofs would need to be calculated again

All other files use u-bl949 or u-bh443 data as in the rest of the repository

Analysis in the Correlations directory didn't really yield any interesting results so is not well formatted at all. It is included for reference,
but should probably be redone more thouroughly if it becomes of interest.

## EOF analysis
EOF analysis is computed using either the eofs.standard package from Ajdawson or xeofs from Nicrie
Both compute eofs using an SVD method and a helpful comparison between what the packages can do can be found in the xeofs documentation.
The main difference used here is the built in rotation function in xeofs, which allowed initial testing of varimax rotations.

Due to the nature of eigenvalues, calculated values work as either the positive or negative, which is why the output PCs are compared to input data,
to ensure the correct sign is used throughout analysis.

## Correlation
Correlation is calculated using the pearsonr function from scipy, which calculates the pearson r value of correlation between two input
sets of data. It is a measure of covariance, meaning that it will be influenced by noise that creates oscillations which are against the trend
of the data.
Because of this, Smooth_comparison_data.ipynb shows an attempt to remove some of the smaller oscillations, particularly those which are less than the
0.5K required to be classified as an ENSO event. Doing this does increase the correlation, so further optimization of the smoothing filter, and perhaps
using one which doesn't overly smooth the data, as fitting to a polynomial here did lose some of the shape of the variation.
