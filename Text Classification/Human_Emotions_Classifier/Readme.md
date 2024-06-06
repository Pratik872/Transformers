# Human Emotions Classifier

## Overview
	- The dataset is downloaded from Huggingface Hub.
	- The dataset is in 'Arrow_Dataset' format containing Train, Validation and Test datasets each having 160000, 2000, 2000 data points respectively.
	- The target labels i.e emotions were 'sadness', 'joy', 'love', 'anger', 'fear', 'surprise'.

## Problem Objective
- To build a model which classifies human emotions based on the tweet they post.

## Methodology

### EDA (Exploratory Data Analysis)
- I have used plots to visualize the data.

![Class_Frequencies](https://github.com/Pratik872/Transformers/blob/main/Text%20Classification/Human_Emotions_Classifier/readme_resources/class_frequencies.png)

- As we see above, there is imbalance in the data.'Joy' and 'Sadness' classes are high and 'surprise' and 'love' are comparatively low.


![Words_per_Tweet](https://github.com/Pratik872/Transformers/blob/main/Text%20Classification/Human_Emotions_Classifier/readme_resources/words_per_tweet.png)

- The maximum context size of DistilBERT model is 512. We have checked above if we have sentences whose token are more than 512. In this dataset, maximum token size doesn't exceed 90. So no need to truncate.

- Required Plots are plotted using matplotlib package.

### Tokenization
- I have tried to implement Character Level, Word Level and Sub-Word level i.e WordPiece used by BERT variants. 

- WordPiece level better suits this used case as it preserves stucture as well as meanings of the tokens.

- Implemented a 'distilbert-base-uncased' tokenizer to tokenize and form input ids for the data.

## <b>Note: </b>Transformers can be used as feature extractors and can be fine-tuned as well. I have implemented both and tried to compare the results

### Transformers as Feature Extractors (just training a classification head keeping hidden states frozen)
- Extracted the hidden states of pre-trained model

- Used those hidden states i.e features to train a Logistic Regression Classifier

- Used hidden state of last '<CLS>' token and passed as an input to logistic classifier

- Got an accuracy of 63%

- Below is the Confusion Matrix:

![Confusion_Matrix_Logistic](https://github.com/Pratik872/Transformers/blob/main/Text%20Classification/Human_Emotions_Classifier/readme_resources/logistic_cm.png)

### Fine-Tuning Distil-BERT

- Fine tuned Distil-BERT with Trainer API

- Batch size of 64, 2 epochs and learning rate as 2e-5

- Got Accuracy 93% and F1 score as 92.5%

- Below is the Confusion Matrix:

![CM_Distil](https://github.com/Pratik872/Transformers/blob/main/Text%20Classification/Human_Emotions_Classifier/readme_resources/DistilBERT_finetuned_cm.png)


### Built with 🛠️
- Packages/Repo : Hugging Face, Transformers, Pandas, Numpy, Matplotlib, Sklearn, Git

- Dataset : Hugging Face Hub

- Coded on : Jupter Notebook (modelling)
