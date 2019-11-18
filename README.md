# Analyzing Presidential Speeches Using Artificial Neural Networks

<img src='/readme_images/main.jpeg'>

When building natural language processing (NLP) classifiers, the goal is usually to identify the class of new, unseen data. This project aims to take this one step further by not only identifying the correct speaker of presidential quotes, but to demonstrate how such an approach can highlight the similarities between presidents. If effective, the project can serve as a proof of concept as to how any group individuals can more more holistically be compared, whether it is modern politicians or other public figures through analysis of social media feeds.

## Data Sources
All data for this project can be found in the folder labeled *Corpus of Presidential Speeches,* which contains over 1,000 raw text files, each of which represents a single speech given by a president. Also included are the general campaign speeches for Donald Trump and Hillary Clinton, though the data does not contain speeches given by Trump since taking office. The original corpus was can be accessed from **[The Grammar Lab](http://www.thegrammarlab.com/?nor-portfolio=corpus-of-presidential-speeches-cops-and-a-clintontrump-corpus)**.

The term *speech* is broadly defined by The Grammar Lab, and may include other forms of public speaking, including debate transcripts. For purposes of this analysis, context of public speech is of little concern, so the corpora was accepted as is.

Speeches are grouped into folders for each president, so folder titles are used as the target variables, with the text files within used as predictor material.

## Approach
The overall approach was developed by using the speech corpora of Donald Trump and Hillary Clinton because of the prominence in modern society. This is important because it allows readers to perform a sort of sanity check to make sure the results actually make sense. In other words, we are more interested in the content as opposed to differences in speech patterns, so we aren't interested in models that achieve higher accuracy scores using the latter approach. Only through a manual spot check of the results can we be sure our models are performing as desired.

A repeatable series of steps was developed to take in data for any two presidents:

1. Select 2 presidents for comparison.
2. Preprocess & tokenize data.
3. Balance datasets.
4. Vectorize tokens.
5. Create benchmark with traditional machine learning models.
6. Build functions that create recurrent and convolutional neural networks.
7. Run gridsearch to find best model using F1-Score.
8. Make predictions with best model & display results with confusion matrix.
9. Create 3 word clouds: one for each president using correct predictions, and one for errors.

Step 9 makes it easier to visualize the words used more explicitly by each individual, while the other allows for a visualization of common themes between them. Resulting word clouds for Donald Trump and Hillary Clinton can be found below.

<img src='/readme_images/DT_HC_diffs.jpeg'>
<img src='/readme_images/DT_HC_sims.jpeg'>

Rather than using graphs to represent these results, we rely on our own intuition to ensure they make sense, taking into account we were able to achieve an accuracy score of 93.1%. The intuition is to make sure our model is differentiating in a way that is useful to us. A more in depth analysis of these visualizations can be found in the analysis itself and relevant blog posts.

## Abstraction
The approach above is illustrated for several pairs of presidents explicitly, but we don't want to have to use a gridsearch and train new neural networks everytime we want to compare two individuals. Instead, we would like to have one model that can analyze the results quickly. In order to do that, we select presidential pairs at random and select one set of hyperparameters at random, and iterate through this process 500 times. All results are saved to a dataframe for further analysis and determine that factors which impact model accuracy most.

As can be seen here, there is great disparity in sample sizes among presidents. What's more, the sample size has the biggest impact on model accuracy, and larger sample sizes make it more likely that deep learning models outperform traditional machine learning models.

<img src='/readme_images/speech_counts.png'>
<img src='/readme_images/speech_counts_accuracy.png'>

In addition, it was observed that RNN's significantly outperformed CNN's, and that Long-Stort Term Memory (LSTM) neurons slightly outperformed Gated Recurrent Units (GRUs). 

<img src='/readme_images/rnn_cnn_compare.png'>

These are only initial observations, but they begin to paint a picture for a way forward.

## Next Steps
The ability to correctly categorize passages from presidential speeches is merely a starting point for something larger. From a prototypical standpoint, we would like an AI that can quickly discern the differences and similarities between any two individuals, and this project presents a way forward. There is a plethora of options to pursue, but a few will be listed here:

1. Generate synthetic data for training to help overcome the problem of sample size.
2. Adapt model to compare 3+ presidents at a time. 
3. Apply machine learning analyses to random selection results to find best neural network hyperparameters.
4. Experiment with different network architectures.

With so many options for pursuing the analysis further, it will require a team of dedicated individuals to achieve the desired results. The ultimate objective here was to present an idea rather than concrete conclusions. However, the analysis itself did seem to warrant a proper conclusion by answering the question: "What do all presidents throughout history have in common?" To answer that, one last word cloud was created, representing common errors in all randomly generated samples. Interpretation of the cloud is left to you:

<img src='readme_images/flag_cloud.png'>