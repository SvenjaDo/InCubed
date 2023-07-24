README: train_model.R

train a random forest model on planet data using all 8 bands plus the 4 calculated indices 

1. setup input paths: 
	- training samples (manually derived from basemap in March 2022. withing ent_004 and ent_005)
		5 Classes: c("Agriculture", "built_up","Forest","road", "Water")
	- enter directory of satellite files and indice files. List all data for ent_004 and ent_005 for the required date.
	- stack and merge all files together to create one dataset for training
2. Training the model: 
	- extract pixel values from raster 
	- split samples into training and testing (90% training, 10% validation
	- create cross-validation folds from training data 
	- set up model settings
	- train the model using parallel processing 
3. model evaluation: 
	- accuracy metrics (plot(model_rf)
	- confusion matrix
	- Variable Importance 
	- visualize predictions on validation data 

the trained model will be stored as model_rf_planet_12bands.rds in the cache folder within working directory. 

-----------------------------------------------------------------------------------------------------------------------------
README: apply_random_forest.R

use trained model to classify the whole dataset.

1. setup output directory and input directory of satellite data and indices data and list all satellite files within directory.
2. load random forest model (model_rf_planet_12bands.rds)
3. run "calc_LC" function providing satellite data, indices data and the RF model to predict the whole dataset
Option A: apply function using lapply
Option B: apply function using parallel processign (way faster!)

the results will be one band .tiff raster files stored in the output directory under "YEAR_DOY_Planet_LC.tif"