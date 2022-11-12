# Emotion-Paraphrasing-Along-Emotion-Gradients
Justin Xie 2022

## About the Experiment
In today's rapidly expanding internet age, more and more of our conversations and communications are done online. Messenger apps such as iMessage or chat rooms such as Discord or Reddit allow users to rapidly and efficiently communicate with each other. However, this new generation of communication comes at a cost. Text online is not accompanied by hand gestures or variations in intonation to signal intensity of emotion. This can lead to miscommunications or misunderstandings as users struggle to decipher what others actually want to convey. In addition, people, in the heat of the moment, often fail to take time to think about their words. They may send overly intense emotions which can lead to unintended consequences.

It is with this is mind, that we decided to tackle the task of Emotion Paraphrasing Along Emotion Gradients. This task involves inputting a short text and paraphrasing it in a way that maintains its meaning but changes its overall tone. For example, this could involve changing a text from anger to annoyance. 

Our approach involves compiling data sets from popular paraphrasing corpuses and using them to train text-to-text transformers using multitask training. The models then can be used to generate paraphrases following an Emotion-Transition Graph that we proposed. The details to the implementation to our approach can be found in this repository. For more details on the experiment, please look at the paper linked in this repository.

## About the Repository 
This repository contains the step-by-step procedural programs needed to perform the task of Emotion Paraphrasing Along Emotion Gradients as described in the paper. The contents of this repository include:

1. `dataset-compilation.ipynb`: Compiles a mix data set from the Google PAWS-Wiki, Microsoft Research Paraphrase, and Quora Question Pairs corpuses. Compiles a twitter data set from the Twitter Language-Net corpus.

2. `mixed-dataset-emotion-labeling.ipynb`: Uses GoEmotions to label and filter the paraphrasing pairs from the mix data set. Generates prefixes using the determined emotion labels for paraphrasing use.

3. `twitter-dataset-emotion-labeling.ipynb`: Uses GoEmotions to label and filter the paraphrasing pairs from the twitter data set. Generates prefixes using the determined emotion labels for paraphrasing use. Splits the twitter data set into a larger training set and a smaller testing set.

4. `combined-dataset-compilation.ipynb`: Creates a combined training and combined testing set with the mix and twitter data sets.

5. `transition-dataset-compilation.ipynb`: Filters the mix, twitter, and combined data sets for only paraphrasing pairs that follow emotion gradients in the Emotion Transition Graph explained int he paper.

6. `fine-tuning-models.ipynb`: Trains T5-base models from the [SimpleTransformers](https://simpletransformers.ai/) package using the compiled data sets. The training can be done using either the regular or limited training function. Regular trains the model on the larger training set and limited trrains the model on the smaller testing set.

7. `model-prediction-generation.ipynb`: Generates predictions on evaluation sets using the trained T5 models.

8. `model-prediction-scoring.ipynb`: Uses GoEmotions to label generated predictions. Uses the generated predictions and their corresponding labeled emotions on [HuggingFace Evaluation Metrics](https://huggingface.co/evaluate-metric) to score the emotion transition and paraphrasing capabilities of the graph.

## Usage of this Repository

#### Prerequisites for Execution
1. You will need to install [Python](https://www.python.org/) 3.7.8 on your computer
2. Parts of the implementation require the [Pandas](https://pandas.pydata.org/), [HuggingFace Evaluation Metrics](https://huggingface.co/evaluate-metric), [SimpleTransformers](https://simpletransformers.ai/), and [Transformers](https://huggingface.co/docs/transformers/main/en/index) packages to run. The SimpleTransformers and Transformers packages will be installed in the Jupyter notebook implementation files due to conflicting Transformer versions. You will need to install the Pandas and Evaluation packages separately. 

```bash
pip3 install pandas
pip3 install evaluate
```

#### Running the Experiment
The order of execution of the implementation is as specified above. 

The data set compilation and emotion labeling done in step 1-4 do not require any user intervention

Step 5 allows the experimenter to choose what data set to train a T5-base model on and the training method (regular or limited) as well as the number of training epochs.

Steps 6-8 allow the experiment to choose the model and the evaluation set in order to generate and score predictions to evaluate the performance of the model on various evaluation sets.


