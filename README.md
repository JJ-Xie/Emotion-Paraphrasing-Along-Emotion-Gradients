# Emotion-Paraphrasing-Along-Emotion-Gradients
Justin Xie 2022

## About the Project

## About the Repository 
This repository contains the step-by-step procedural programs needed to perform the task of Emotion Paraphrasing Along Emotion Gradients as described in the paper. The contents of this repository include:

1. `dataset-compilation.ipynb`: Compiles a mix data set from the Google PAWS-Wiki, Microsoft Research Paraphrase, and Quora Question Pairs corpuses. Compiles a twitter data set from the Twitter Language-Net corpus.

2. `mixed-dataset-emotion-labeling.ipynb`: Uses GoEmotions to label and filter the paraphrasing pairs from the mix data set. Generates prefixes using the determined emotion labels for paraphrasing use.

3. `twitter-dataset-emotion-labeling.ipynb`: Uses GoEmotions to label and filter the paraphrasing pairs from the twitter data set. Generates prefixes using the determined emotion labels for paraphrasing use. Splits the twitter data set into a larger training set and a smaller testing set.

4. `combined-dataset-compilation.ipynb`: Creates a combined training and combined testing set with the mix and twitter data sets.

5. `transition-dataset-compilation.ipynb`: Filters the mix, twitter, and combined data sets for only paraphrasing pairs that follow emotion gradients in the Emotion Transition Graph explained int he paper.

6. `fine-tuning-models.ipynb`: Trains T5-base models from the [SimpleTransformers](https://simpletransformers.ai/) package using the compiled data sets.

7. `model-prediction-generation`: Generates predictions on evaluation sets using the trained T5 models.

8. `model-prediction-scoring`: Uses GoEmotions to label generated predictions. Uses the generated predictions and their corresponding labeled emotions on [HuggingFace Evaluation Metrics](https://huggingface.co/evaluate-metric) to score the emotion transition and paraphrasing capabilities of the graph.
