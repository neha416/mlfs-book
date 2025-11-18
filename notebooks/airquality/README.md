## Project Overview

This project predicts PM2.5 air quality levels for Stockholm (St-Eriksgatan-83) using historical weather and air-quality data.

It demonstrates building a complete machine learning workflow including:
*	Backfilling historical data
*	Daily feature pipeline
*	Training pipeline
*	Batch inference pipeline
*	Dashboard generation (forecast + hindcast)
*	Model registry integration

The system is built using:
*	XGBoost regression model
*	Hopsworks Feature Store
*	Hopsworks Model Registry
*	GitHub Actions automation
*	Open-Meteo API for weather data
*	AQICN API for air quality

## Steps Performed

1. **Feature Backfill**: Historical weather and air quality data were loaded into the Hopsworks Feature Store.
2. **Daily Feature Pipeline**: A daily pipeline automatically downloads yesterday’s air-quality and weather data along with a 7–10 day weather forecast, and updates the Feature Groups through GitHub Actions.
3. **Training Pipeline**: Selected features were used to train an XGBoost model for PM2.5 prediction.
4. **Batch Inference**: Forecasts were generated for the next 7–10 days and saved as PNG dashboards.
5. **Monitoring**: Hindcast graphs were created comparing predictions vs actual PM2.5 values.
6. **Grade C Feature** : Lagged PM2.5 features (1, 2, 3 days) were added to improve model performance.

**Improvement**: Lagged PM2.5 Features
 To improve the model, three new lag features were added:
* Feature	Meaning
pm25_lag_1	PM2.5 value 1 day earlier
pm25_lag_2	PM2.5 value 2 days earlier
pm25_lag_3	PM2.5 value 3 days earlier
 A new model (Version 2) was trained using these additional features.

## Performance Comparison
* Old Model (Version 1):
MSE: 145.6693  
R²: -0.5223629400897112
* New Model (Version 2 with lag features):
MSE: 144.53683  
R²: -0.5200045264066999

* Explanation
Adding lag features (previous days’ PM2.5 values) slightly improved the model. This is expected because air pollution tends to follow recent trends, and weather alone does not fully explain it. Including past PM2.5 levels gives the model more context, helping it make better predictions.
 Note: R² is still negative, which means the model is not very accurate yet and performs worse than just predicting the average.

## Results
The project outputs:
* Forecast dashboard showing future PM2.5 predictions
* Hindcast dashboard showing prediction vs actual accuracy
* Model artifacts stored in Hopsworks Model Registry (Version 1 and Version 2)
These visualizations allow tracking how well the model performs and how predictions evolve over time.


## Repository Structure
**notebooks/airquality/** – contains:
* 	1_air_quality_feature_backfill.ipynb
* 	2_air_quality_feature_pipeline.ipynb
* 	3_air_quality_training_pipeline.ipynb
* 	4_air_quality_batch_inference.ipynb
* 	5_function_calling.ipynb
* 	notebooks/airquality/air_quality_model/ – trained model files and generated images
* 	docs/air-quality/assets/img/ – dashboard images
* 	README.md – project description and explanation



•
