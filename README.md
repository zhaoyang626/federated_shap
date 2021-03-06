# federated_shap

Code for paper ["Interpret Federated Learning with Shapley Values"](https://arxiv.org/abs/1905.04519)

[中文blog](http://www.crownpku.com/2019/05/18/%E7%94%A8Shapley%E5%80%BC%E8%A7%A3%E9%87%8A%E8%81%94%E9%82%A6%E5%AD%A6%E4%B9%A0%E6%A8%A1%E5%9E%8B.html)


### Calculate SHAP values for Federated Features

Inspired by SHAP: https://github.com/slundberg/shap



### Input of federated_shap:


**f**: model function, inputs a instance and outputs a prediction value.

**x**: numpy array, target instance with features to be interpreted.

**reference**: numpy array, to determine the impact of a feature, that feature is set to "missing" and the change in the model output is observed. Since most models aren't designed to handle arbitrary missing data at test time, we simulate "missing" by replacing the feature with the values it takes in the background dataset. So if the background dataset is a simple sample of all zeros, then we would approximate a feature being missing by setting it to zero. For small problems this background dataset can be the whole training set, but for larger problems consider using a single reference value or using the kmeans function to summarize the dataset.

**M**: integer, number of features

**fed_pos**: integer, feature position in x starting from which the features are hidden and united
 

### Usage of federated_shap:

```
import federated_shap
fs = federated_shap.federated_shap()
# shap
shap_values = fs.kernel_shap(f_knn, x, med, M)[:-1]
# federated shap
shap_values_federated = fs.kernel_shap_federated(f_knn, x, med, M, fed_pos)[:-1]
```

### Results

Plot for Feature Importance (Shapley values) for 1000 random predictions. Top figure is for the
whole feature space, middle figure is for federated feature of last 3 features, and bottom figure is for federated feature of last 5 features.

![](/img/result.png)
