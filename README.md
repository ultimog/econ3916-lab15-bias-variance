# econ3916-lab15-bias-variance
# The Bias-Variance Tradeoff: Choosing How Flexible a Model Should Be

## Objective
I tested how a model's flexibility affects its error on new data, and how to choose that flexibility without seeing the true curve.

## Methodology
- In a simulated world with a known true curve, I split the error of polynomial fits into bias squared and variance, using 200 fresh samples at each of six degrees.
- I compared training error with error on 2,000 new points for degrees 1 to 15, and found the degree where the held-out error was lowest.
- I chose a degree by 5-fold cross-validation, and looked at how much the error varied from fold to fold.
- I used nested cross-validation to check whether the smallest CV error is a fair estimate of the error on new data.
- I wrote a small function, kfold_mse(), that gives the k-fold CV error for any degree and number of folds, and checked it with 10 folds.
- I drew learning curves for a degree-9 polynomial as the training set grew from 20 to 2,000 points.
- I fitted minimum-norm polynomials up to degree 991 to see what happens past the point where the model can pass through every training point.

## Key Findings
- Variance was 0.0180 at degree 5 and 0.0994 at degree 15, while bias squared fell to almost zero by degree 9.
- Training error fell at every degree, but held-out error was lowest at degree 5, so training error can't tell you where to stop.
- 5-fold CV chose degree 4, with a CV MSE of 0.1401.
- Nested CV estimated the error at 0.2070, higher than the 0.1401, because picking the smallest of several CV scores is too optimistic.
- With 10 folds, the CV MSE was 0.1409 for degree 4 and 0.1457 for degree 5, the same ranking as with 5 folds.
- With more data, the gap between training and held-out error closed, from 0.08 against 73.8 at 20 points to about 0.20 for both at 2,000: more data fixes variance, not noise.
- Past the interpolation point, the held-out error of the minimum-norm fit peaked near degree 51 and then fell again, to 0.32 at degree 991 (double descent), but never beat 0.28 at degree 11.
