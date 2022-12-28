# cms_machinelearning

This was a project I completed for CIS 4130 Big Data class in Baruch.
Class focused on using EC2 instance, S3 Bucket, and AWS EMR (PySpark)

The goal was to see if the amount that Original Medicare pays to physicians can be accurated predicted using a linear regression model using:
the amount of Medicare beneficiaries, the amount of doctors, and which state.

The instructions are all in the final code text, including where the data was obtained.
The EDA for the combined 6 years data is in the eda text.
The predictions result from the machine learning model is in the predictions text.
There are four visualizations as well.

The linear regression model was awful with the predictor variables selected:
RMSE is extremely high in proportion to the paid amounts
R^2 value is only around 4%


