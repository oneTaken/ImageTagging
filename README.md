# ImageTagging
project results demo. Already transferred on Android app.

This is a similar edition of Apple's Photo Classification function.

- [function](#function)
- [Dataset details](#dataset-details)
- [confusion matrix](#confusion-matrix)
- [prediction time analysis](#prediction-time-analysis)
- [test case](#test-case)
#  function
+ Give a searching class name, then predict all the photos and cluster and copy all the photos
matching the class to a new folder.
+ Give a new photo, then predicate the photo and return the predicted class names.
Finally give the user a option to choose which class name to classify into.
#  dataset details
The origin datasets has ~130w images and 21 classes.
Some modification on the origin dataset:
+ Remove 3 too abstract classes
+ Merge some similar classes
+ Add people class Using MicroSoft Face Detection API

|phase|percent|image number|
|:------:|:-----:|:----:|
|total|100|809070|
|train|90|728165|
|valid|1|8099|
|test|9|72815|
Tips: The percent is used to choose random samples on every single class to keep 
data balanced as much as possible. And actually, every class has a loss weight which 
is the invert percent of the class image number of the total image number.
We also tried manually choose the loss weight as a super parameter. We manually 
enlarge the loss weight for the people class to try to get better performance on the 
people class. The results didn't show coherent improvement under some tries. 

# confusion matrix
|Vgg19_bn|mobilenet|
|----|-----|
|![](./analysis/vgg_confusion_matrix.png)|![](./analysis/mobile_confusion_matrix.png)


# prediction time analysis
The measure is always second(s), it's an average of 100 times.

|name|init time|load time|cpu|gpu|
|:-----:|:-----:|:-----:|:-----:|:-----:|
|mobilenet|0.0545|0.0178|0.3811|0.1786|
|vgg19_bn|1.709|3.584|1.308|0.006|

# test case
