# Natural Language Processing 

This project is devoted to the question-answering task on **BoolQ** dataset from SuperGLUE. BoolQ is a question answering dataset for yes/no.

Solution consists of the following steps:
1. Data analysis;
2. Pretrained embeddings as features for classifier (please, refer to Jupyter notebook for details):
- word2vec,
- BERT embeddings;
3. Fine-tune BERT;
4. Summary & results analysis.

Conclusion to the project:
### 4. Summary & results analysis


#### 4.1. Compare the results


Let us populate the following `table 1` with all the data we obtained.

Table 1

|id|Model|Vectorizer|Corpus|Accuracy|
|--|:--|:--:|:--:|:--:|
|1|SVM|word2vec|BoolQ|0.63|
|2|SVM|BERT|BoolQ|0.62|
|3|BERT (fine-tuned)|BERT|BoolQ|0.68|

**SVM** trained on the sentence embeddings produced by word2vec model demonstrated slightly better result than **SVM** trained on BERT produced embeddings (with the same parameters of the classifiers). Frankly speaking, before the experiment I expected that result of classification for BERT embeddings would be better, since BERT takes the context into account. Probably it would be good to fine-tune **SVM** classifier by Grid search for example, but this is quite a time consuming process and it is out of scope of the task.

On the same corpus (BoolQ) fine-tuned BERT classification model demonstrated slightly higher results than initial BERT and word2vec based classifiers.

Let us populate the following `table 2` with the results provided by the authors of the [paper](https://arxiv.org/abs/1905.10044), our task is based on.

Table 2

|Rank|Model|Accuracy, %|
|:--:|:--|:--:|
|1|**Human annotators**|90|
|2|**BERT (fine-tuned)**|80.4|
|3|**majority-baseline**|62|


Comparing tables 1 and 2, we may come to the conclusion that our BERT (trained on BoolQ) demonstrated quite good accuracy, but our result (68%) is expectedly not even close to the accuracy achieved by the authors of the paper (80.4%).

#### 4.2. Way of possible improvement of the model score

Due to lack of computational resources I had to use GPU provided free of charge by Google Colab. Practically GPU was available only for an hour and a half during the day. Therefore, I was limited with number of epochs to set for the trainig purposes.
I believe there are at least 3 ways to improve the quality metric of the model:
- use different concatenation technique (we used a sum of the sentence vectors for `question` and `passage`);
- try to use another optimizer to obtain a minimum of the loss function more accurately;
- extend training dataset.
