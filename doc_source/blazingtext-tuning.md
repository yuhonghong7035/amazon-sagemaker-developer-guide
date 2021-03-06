# Tuning a BlazingText Model<a name="blazingtext-tuning"></a>

*Automatic model tuning*, also known as hyperparameter tuning, finds the best version of a model by running many jobs that test a range of hyperparameters on your dataset\. You choose the tunable hyperparameters, a range of values for each, and an objective metric\. You choose the objective metric from the metrics that the algorithm computes\. Automatic model tuning searches the hyperparameters chosen to find the combination of values that result in the model that optimizes the objective metric\.

For more information about model tuning, see [Automatic Model Tuning](automatic-model-tuning.md)\.

## Metrics Computed by the BlazingText Algorithm<a name="blazingtext-metrics"></a>

The BlazingText Word2Vec algorithm \(`skipgram`, `cbow`, and `batch_skipgram` modes\) reports on a single metric during training: `train:mean_rho`\. This metric is computed on [WS\-353 word similarity datasets](https://www.cs.technion.ac.il/~gabr/resources/data/wordsim353/)\. When tuning the hyperparameter values for the Word2Vec algorithm, use this metric as the objective\.

BlazingText Text Classification algorithm \(`supervised` mode\), also reports on a single metric during training: the `validation:accuracy`\. When tuning the hyperparameter values for the text classification algorithm, use this metrics as the objective\.


| Metric Name | Description | Optimization Direction | 
| --- | --- | --- | 
| train:mean\_rho |  Mean rho \(Spearman's rank correlation coefficient\) on [WS\-353 word similarity datasets](https://www.cs.technion.ac.il/~gabr/resources/data/wordsim353/)\.  |  Maximize  | 
| validation:accuracy |  Classification accuracy on user specified validation dataset\.  |  Maximize  | 

## Tunable BlazingText Hyperparameters<a name="blazingtext-tunable-hyperparameters"></a>

### Tunable Hyperparameters for Word2Vec<a name="blazingtext-tunable-hyperparameters-word2vec"></a>

Tune the Amazon SageMaker BlazingText Word2Vec model with the following hyperparameters\. The hyperparameters that have the greatest impact on Word2Vec objective metrics are: `mode`, ` learning_rate`, `window_size`, `vector_dim`, and `negative_samples`\.


| Parameter Name | Parameter Type | Recommended Ranges | 
| --- | --- | --- | 
| mode |  CategoricalParameterRange  |  \['batch\_skipgram', 'skipgram', 'cbow'\]  | 
| learning\_rate |  ContinuousParameterRange  |  MinValue: 0\.005, MaxValue: 0\.01  | 
| min\_count |  IntegerParameterRange  |  \[0\-100\]  | 
| window\_size |  IntegerParameterRange  |  \[1\-10\]  | 
| vector\_dim |  IntegerParameterRange  |  \[32\-300\]  | 
| epochs |  IntegerParameterRange  |  \[5\-15\]  | 
| negative\_samples |  IntegerParameterRange  |  \[5\-25\]  | 
| batch\_size |  IntegerParameterRange  |  \[8\-32\]  | 
| sampling\_threshold |  ContinuousParameterRange  |  MinValue: 0\.0001, MaxValue: 0\.001  | 

### Tunable Hyperparameters for Text Classification<a name="blazingtext-tunable-hyperparameters-text_class"></a>

Tune the Amazon SageMaker BlazingText Text Classification model with the following hyperparameters\.


| Parameter Name | Parameter Type | Recommended Ranges | 
| --- | --- | --- | 
| mode |  CategoricalParameterRange  |  \['supervised'\]  | 
| min\_count |  IntegerParameterRange  |  \[0\-100\]  | 
| learning\_rate |  ContinuousParameterRange  |  MinValue: 0\.005, MaxValue: 0\.01  | 
| vector\_dim |  IntegerParameterRange  |  \[32\-300\]  | 
| epochs |  IntegerParameterRange  |  \[5\-15\]  | 
| word\_ngrams |  IntegerParameterRange  |  \[1\-3\]  | 
| buckets |  IntegerParameterRange  |  \[1000000\-10000000\]  | 