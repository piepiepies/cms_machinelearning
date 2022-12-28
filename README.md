# cms_machinelearning

This was a project I completed for CIS 4130 Big Data class in Baruch
The goal was to see if the amount that Original Medicare pays to physicians can be accurated predicted using a linear regression model using:
the amount of Medicare beneficiaries, the amount of doctors, and which state

The instructions are all in the final code text, including where the data was obtained.
There are four visualizations as well. 

EDA for the combined 6 years data:
RangeIndex: 58610641 entries, 0 to 58610640
Data columns (total 9 columns):
 #   Column                     Dtype  
---  ------                     -----  
 0   Rndrng_NPI                 object 
 1   Rndrng_Prvdr_City          object 
 2   Rndrng_Prvdr_State_Abrvtn  object 
 3   Rndrng_Prvdr_Cntry         object 
 4   Tot_Benes                  int64  
 5   Tot_Srvcs                  float64
 6   Avg_Sbmtd_Chrg             float64
 7   Avg_Mdcr_Alowd_Amt         float64
 8   Avg_Mdcr_Pymt_Amt          float64
dtypes: float64(4), int64(1), object(4)
memory usage: 3.9+ GB
--------------
shape is (58610641, 9)
--------------
size is 527495769
--------------
          Tot_Benes     Tot_Srvcs  Avg_Sbmtd_Chrg  Avg_Mdcr_Alowd_Amt  Avg_Mdcr_Pymt_Amt
count  5.861064e+07  5.861064e+07    5.861064e+07        5.861064e+07       5.861064e+07
mean   8.720181e+01  2.483465e+02    3.554180e+02        1.002001e+02       7.834937e+01
std    1.182859e+03  5.841082e+03    1.087017e+03        2.761212e+02       2.202187e+02
min    1.100000e+01  2.400000e+00    3.333330e-05        0.000000e+00       0.000000e+00
25%    1.700000e+01  2.000000e+01    5.977889e+01        2.325000e+01       1.893500e+01
50%    3.200000e+01  4.300000e+01    1.480000e+02        6.419706e+01       4.778929e+01
75%    7.400000e+01  1.170000e+02    3.000000e+02        1.120545e+02       8.596500e+01
max    9.186660e+05  1.129063e+07    9.999999e+04        5.577743e+04       4.443910e+04
--------------
Rndrng_NPI                      0
Rndrng_Prvdr_City            1688
Rndrng_Prvdr_State_Abrvtn       0
Rndrng_Prvdr_Cntry              0
Tot_Benes                       0
Tot_Srvcs                       0
Avg_Sbmtd_Chrg                  0
Avg_Mdcr_Alowd_Amt              0
Avg_Mdcr_Pymt_Amt               0
dtype: int64
--------------
total null values are 1688

#showing the results
predictions.select('Rndrng_Prvdr_State_Abrvtn', 'Tot_Benes', 'doctors', 'prediction', 'label').show(10)

+-------------------------+---------+-------+------------------+------------------+
|Rndrng_Prvdr_State_Abrvtn|Tot_Benes|doctors|        prediction|             label|
+-------------------------+---------+-------+------------------+------------------+
|                       AK|       11|   2256|264367.06859588425|1870662.4300021096|
|                       AK|       12|   2256|264371.63525865244|1491597.3099992708|
|                       AK|       16|   2256| 264389.9019097254| 1582329.199998182|
|                       AK|       19|   2256|264403.60189803015| 1415598.330000146|
|                       AK|       22|   2256|264417.30188633484|   1324619.8899982|
|                       AK|       26|   2256| 264435.5685374078| 984342.6800060247|
|                       AK|       33|   2256| 264467.5351767855| 900823.6299997562|
|                       AK|       36|   2256| 264481.2351650902| 693320.5400023448|
|                       AK|       38|   2256| 264490.3684906267| 627108.3999992366|
|                       AK|       39|   2256|264494.93515339494| 776688.7199995685|
+-------------------------+---------+-------+------------------+------------------+
only showing top 10 rows

#18 models
print(len(cvModel.avgMetrics))
18

#average of each of the 18 models from the parameters between the 3 folds
for metrics in cvModel.avgMetrics:
	print(metrics)

3281365.069748538
3281365.069748538
3281365.069748538
3281365.0688539506
3281369.821513733
3281386.060373017
3281365.0672560427
3281386.060624458
3281383.3777453653
3281365.065658364
3281381.525604812
3281382.455128671
3281365.064060915
3281383.3782805298
3281386.863797317
3281365.062463692
3281383.078159724
3281380.567631323

#rmse of the best model
rmse = modelEvaluator.evaluate(predictions)
print(rmse)
3283240.5443320866

#r2 of the best model
r2evaluator = RegressionEvaluator(metricName='r2')
r2=r2evaluator.evaluate(predictions)
print(r2)
0.04104794100418885

The linear regression is below subpar.
RMSE value is huge in proportion to the paid amounts.
R^2 value is extremely low.

