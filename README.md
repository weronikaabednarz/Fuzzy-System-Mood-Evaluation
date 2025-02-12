# Analysis of the possibility of using recurrent neural networks to generate new melodies based on the MIDI files

## About project
The aim of the project was to develop a fuzzy system for assessing the mood of musical pieces based on their acoustic characteristics, 
such as **energy**, **valence** (level of emotion - emotional charge) and **danceability**. The developed algorithm is able to determine 
the **mood of a song** (sad, neutral, happy) by analysing these parameters.

The system allows the music to be better matched to the listener's emotions, which can influence the listener's experience and create more 
personalised playlists, as well as support music therapies.

## Dataset
The **dataset** used is from the kaggle platform:
https://www.kaggle.com/datasets/soumikrakshit/classical-music-midi includes works by 19 different composers performed on the piano. 
I chose pieces composed by Frederic Chopin to train the model.

## Technologies
The project was implemented using **Python** in the **Google Colab** environment.

**Libraries** used in the project:
- numpy - operations on arrays, matrices and vectors,
- pandas - processing of tabular data,
- matplotlib.pyplot - creating graphs,
- seaborn - data visualisation, supporting matplotlib,
- google.colab - environment for running Python code in the cloud, particularly useful for data analysis and machine learning,
- Ipywidgets - A library to create interactive widgets in Jupyter notebooks for user interaction,
- IPython.display - displaying images and sounds,
- mpl_toolkits.mplot3d - A tool in Matplotlib for creating 3D graphs,
- scikit-fuzzy - Library for implementing fuzzy systems and fuzzy algorithms in Python.

## Descriptive characteristics of input and output variables
**Input variables:**
- **Energeticity**: represents the intensity of the music (low, medium, high), measured by signal amplitude analysis.
- **Emotional charge**: represents the level of emotion expressed in the music (from depressive to euphoric). Obtained by analysing the tonality, harmony and chord structure of the piece.
- **Danceability**: determines how danceable the piece is, based on the rhythm and tempo of the piece. This is a variable that can be analysed using rhythm analysis tools.

**Output variables:**
- **Mood**: determines what emotion the piece evokes (sad, neutral or happy).

## Images
**Dataset:**

![1](./images/used_dataset.jpg)

![2](./images/melodies_used.jpg)

**Appearance of the interface for generating new melodies:**

![3](./images/interface.jpg)

The interface created allows the user to easily adjust the parameters of the melody, such as:
- **duration of the song** (in seconds) using a slider,
- **tempo** selected from a drop-down list (slow, moderate, fast).

This solution allows new melodies to be dynamically generated without having to look into the code.

**Model configurations included:**

![4](./images/melody_evaluation_metrics.jpg)

**Results for selected model evaluation metrics:**

![5](./images/model_evaluation_metrics.jpg)

Analysis of the training times showed a significant difference between the **shortest and longest times**. The shortest time was 16 minutes (Model 30), while the longest time reached 358 minutes (Model 26). This difference highlights the variation in performance of the models used in the experiments. Training time increases approximately linearly with the number of epochs, which is expected. Models trained for 100 epochs (e.g. Model 14, Model 15) have significantly longer training times compared to those trained for 10 or 50 epochs.

A higher dropout (e.g. 0.5 in Model 15, 17, 27, 40) leads to an increase in the regularity of the model, which helps to avoid overfitting. These models maintain stable performance on the test set, but may have difficulty learning more complex patterns.
For both the training and test set, lower values of the **Cross-Entropy Loss** function indicate better model fit. Analysing the results obtained, it can be seen that models consisting of two LSTM layers and smaller dropout values achieve the lowest values for this metric - for example, model 14 and model 26. Furthermore, models trained for a higher number of epochs (100) tend to achieve lower Cross Entropy Loss values.

The values of the Cross-Entropy Loss and Perplexity metrics are correlated. Models characterised by a low value of **Perplexity** for the test set are more predictable and generalise better, which means that the difference between the results for the two sets is small.
When considering the results obtained, it can be seen that the lowest values on the training set for this metric are obtained by models: 13, 14, 18, 26, 36 and 37, but these values for the test set are already much higher for these models, which may indicate a tendency towards overlearning. In contrast, satisfactory Cross-Entropy Loss and Perplexity results for the training and test set were obtained for models: 8, 15, 16, 17, 40. Considering in the evaluation of the models also the **Cosine Similarity** metric, whose higher values indicate a better representation of the similarity between the model predictions and the actual data, it can be seen that model 8 obtained very poor results.

From the results obtained, it can be concluded that **model number 16** achieves the most satisfactory results of all the models analysed. It is characterised by a relatively low difference in Cross-Entropy Loss and Perplexity values between the training set and the test set, indicating good generalisability. In addition, the very high value of the Cosine Similarity metric suggests that the model is a good fit to the data. It is particularly noteworthy that such good results were obtained with a dropout of 0.3, which helps to reduce the risk of overfitting.

**Results for selected metrics for evaluating the generated melodies:**

![6](./images/melody_evaluation_metrics.jpg)
