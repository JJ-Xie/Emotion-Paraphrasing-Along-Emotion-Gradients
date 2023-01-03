# Fine-Grained Emotional Paraphrasing along Emotion Gradients
Justin Xie 

November 15, 2022

## Overview
In today's rapidly expanding internet age, more and more of our conversations and communications are done online. Messenger apps such as iMessage or chat rooms such as Discord or Reddit allow users to rapidly and efficiently communicate with each other. However, this new modality of communication comes at a cost. Text communciations online are not accompanied by hand gestures or variations in intonation to signal intensities of emotion. This can lead to miscommunications or misunderstandings as users struggle to decipher what others actually want to convey. In addition, people, in the heat of the moment, often fail to take time to think about their words. They may send overly intense emotions which can lead to unintended consequences.

With this challenge in mind, we decided to tackle the task of Fine-Grained Emotion Paraphrasing along Emotion Gradients. This task involves inputting a short text and paraphrasing it in a way that maintains its meaning but changes its overall tone. For example, this could involve changing a text from anger to annoyance. 

Our approach involves compiling data sets from popular paraphrasing corpuses and using them to train text-to-text transformers using multitask training. The models can then be used to generate paraphrases following an Emotion-Transition Graph that we proposed. The details of the implementation to our approach can be found in this repository. For more details on the experiment, please look at the paper linked in this repository.

## About the Repository 

#### Execution Files
This repository contains the step-by-step procedural programs needed to perform the task of Fine-Grained Emotion Paraphrasing along Emotion Gradients as described in the paper. The programs in this repository are run in the following order to execute the experiment:

`1-dataset-compilation.ipynb`: Compiles a mixed data set from the Google PAWS-Wiki, Microsoft Research Paraphrase, and Quora Question Pairs corpuses. Compiles a Twitter data set from the Twitter Language-Net corpus.

`2-mixed-dataset-emotion-labeling.ipynb`: Uses GoEmotions to label and filter the paraphrasing pairs from the mixed data set. Generates prefixes using the determined emotion labels for paraphrasing use.

`3-twitter-dataset-emotion-labeling.ipynb`: Uses GoEmotions to label and filter the paraphrasing pairs from the Twitter data set. Generates prefixes using the determined emotion labels for paraphrasing use. Splits the Twitter data set into a larger training set and a smaller test set.

`4-combined-dataset-compilation.ipynb`: Creates a combined training set and a combined test set from the mixed and Twitter data sets.

`5-transition-dataset-compilation.ipynb`: Filters the mixed, Twitter, and combined data sets for only paraphrasing pairs that follow emotion gradients in the Emotion Transition Graph explained in the paper.

`6-fine-tuning-models.ipynb`: Fine-tunes T5-base models from the [SimpleTransformers](https://simpletransformers.ai/) package using the compiled data sets. The training can be done using either the regular or limited training function. Regular trains the model on the larger training set and limited trains the model on the smaller test set.

`7-model-prediction-generation.ipynb`: Generates predictions on evaluation sets using the fine-tuned T5 models.

`8-model-prediction-scoring.ipynb`: Uses GoEmotions to label generated predictions. Uses the generated predictions and their corresponding labeled emotions to score the emotion transition and paraphrasing capabilities of the fine-tuned models, on [HuggingFace Evaluation Metrics](https://huggingface.co/evaluate-metric).

`dataset-filter-compilation`: Uses VADER intensity scores and GoEmotion groupings to create filter levels for dataset filtering.

`new-fine-tuning`: Adds filter choices to the fine-tuning process and adds a section of code to fine-tune a GPT-2 model.

`new-model-prediction-generation`: Adds filter choices to the prediction generation process and adds a section of code to generate prediction from a fine-tuned GPT-2 models.

`new-model-prediction-scoring`: Adds filter choices to the prediction scoring process and adds a section of code to score predictions by a fine-tuned GPT-2 models.

`few-shot-dataset-splitting`: Splits larger dataset into subsets for consistent few-shot fine-tuning.

#### Other Files
- `GoEmotions/`: Contains the GoEmotions Emotion Classifier with our modification. Details about GoEmotions can be found [here](https://arxiv.org/pdf/2005.00547.pdf)

- `utils.py`: Contains utility functions for cleansing data sets. 

## Usage of This Repository

#### Depedencies
1. You will need to install [Python](https://www.python.org/) 3.7.8 on your computer. 
2. Parts of the implementation require the [Pandas](https://pandas.pydata.org/), [HuggingFace Evaluation Metrics](https://huggingface.co/evaluate-metric), [SimpleTransformers](https://simpletransformers.ai/), and [Transformers](https://huggingface.co/docs/transformers/main/en/index) packages to run. The SimpleTransformers and Transformers packages will be installed in the Jupyter notebook implementation files respectively due to conflicting Transformer versions. You will need to install the Pandas and Evaluation packages separately. 

```bash
pip3 install pandas
pip3 install evaluate
```

#### Running Our Workflow 
The execution order of our workflow is as specified above. 

To start, unzip both the mixed data set and the two halves of the twitter data set.

The data set compilation and emotion labeling in steps 1-4 do not require any user intervention.

Step 5 allows the user to choose which data set to train a T5-base model on and the training method (regular or limited) as well as the number of training epochs.

Steps 6-8 allow the user to choose the model and the evaluation set in order to generate and score predictions to evaluate the performance of the models fine-tuned on various evaluation sets.
