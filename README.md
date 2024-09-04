# Maji Ndojo National Water Survey Analysis
## Part 1 Visualizing Maji ndogo's Past
***
![](./images/capture1.png)
***

### Contents
- [Project Overview](#project_overview)
- [Features](#features)
- [Findings](Findings)
- [Leason Learned] (leason_learned)

***

**Author**: 
* [Kelvin SIla](https://github.com/ksila01)
***
  
## Project_Overview
This project is the first part of the Maji Ndogo Integrated Water Project, focusing on visualizing the historical aspects of water access in the Maji Ndogo region. The goal of this visualization is to provide insights into past water access challenges, helping stakeholders understand the trends, patterns, and key issues that have shaped the current situation. By leveraging Power BI, this project presents data in an interactive and visually engaging manner to support informed decision-making and future interventions.

***

**Features**
* **Historical Data Visualization**: Interactive dashboards that present historical data on water access, including gender disparities, regional differences, and crime patterns related to water collection.
* **Customizable Filters**: Users can apply various filters to explore specific aspects of the data, such as time periods, geographic regions, and demographic groups.
* **Engaging Visuals**: The report includes a variety of visualizations, such as maps, pie charts, and trend lines, to effectively convey the key findings.

**National Statistics**

![Alt Text](images/question_response_lengths_histogram.png)

**Findings**
* The blue bars (questions) are clustered more towards the left side of the graph, indicating that most questions are shorter in length. The tallest blue bar, indicating the highest frequency, falls in the range of 0-10 words approximately.
* The red bars (responses) show a wider distribution across the word count, suggesting that responses have a more varied length. The tallest red bar is in the range of 10-20 words.
* The blue bars (questions) have a peak frequency much higher than the red bars (responses), suggesting that there is a common word count range where most questions fall.

**Word Frequency Analysis**

![Alt Text](images/most_common_words_bar_chart.png)

**Word Cloud**
![Alt Text](images/Capture.PNG)

**Findings**
* The analysis provides insights into the key themes and topics present in the dataset.
* The most common words reflect a strong emphasis on courses, data science, Moringa, and educational aspects.
* With 'course' being the most frequent word, the dataset places a substantial emphasis on educational offerings.
* 'data,' 'science,' and 'moringa' indicate a strong focus on data science education, aligning with industry and institutional themes.
* The repetition of terms like 'student,' 'develop,' and 'learn' underscores a learner-centric approach in the dataset.
**Bi-grams and Tri-grams Analysis**
![Alt Text](images/most_common_ngrams_subplot.png)

**Findings**

* On the left, the bi-grams bar chart shows that "data science" is the most frequent bi-gram, followed by "moringa school" and others.
* On the right, the tri-grams bar chart indicates "data science course" as the most frequent tri-gram, with a notable drop in frequency for subsequent tri-grams

***
## Modeling

**Base Model Performance**

![Alt Text](images/base_model.png)
![Alt Text](images/base_model1.png)

**Findings**
*The base model demonstrates a high training accuracy of approximately 98%, suggesting effective learning from the training data*.
*However, a significant performance gap is observed, with the validation accuracy plateauing at 30-40%, raising concerns about overfitting*.
*The validation loss notably increases in later epochs, reaching around 9.8, further reinforcing overfitting concerns*.
*To address these issues, recommendations include incorporating both questions and responses in the training data for a more comprehensive understanding, implementing regularization techniques to mitigate overfitting, and exploring performance improvement measures such as learning rate tuning and optimizing hidden layers*.
*Additionally, testing different vectorization methods like TFIDF and embeddings is suggested, with the option to consider alternative deep learning models if necessary*.

**Train on both questions and responses**

![Alt Text](images/model.png)
![Alt Text](images/model1.png)

**Findings**
*The model exhibits notable improvement, with training accuracy at approximately 99.42% and validation accuracy at around 58.78%*.
*Despite this progress, there is potential for further enhancement in the validation accuracy*.

**Regularization - Dropout regularization**

![Alt Text](images/model2.png)
![Alt Text](images/model3.png)
**Optimize the number of hidden layers:**

![Alt Text](images/model4.png)
![Alt Text](images/model5.png)

**Term Frequency * Inverse Document Frequency (TFIDF) vectorization**

![Alt Text](images/model6.png)
![Alt Text](images/model7.png)

***

## Evaluation

***
This model is a feedforward neural network with multiple hidden layers. Here's a summary of its architecture and training performance:

1. **Architecture**:
   - Input Layer: 
     - Dense layer with 128 neurons, using the hyperbolic tangent (tanh) activation function. Regularized with L2 regularization with a regularization parameter of 0.01.
     - Dropout layer with a dropout rate of 0.8 to prevent overfitting.
   - Hidden Layers:
     - Dense layer with 64 neurons, using the tanh activation function.
     - Dropout layer with a dropout rate of 0.5.
     - Dense layer with 150 neurons, using the tanh activation function.
     - Dropout layer with a dropout rate of 0.5.
   - Output Layer:
     - Dense layer with the number of neurons equal to the number of classes (output categories), using the softmax activation function.
   - Model is compiled with categorical cross-entropy loss function and Stochastic Gradient Descent (SGD) optimizer with a learning rate of 0.001, momentum of 0.9, and Nesterov momentum.

2. **Training Performance**:
   - The model is trained for 250 epochs with a batch size of 5.
   - Throughout training, the loss decreases steadily, indicating that the model is learning to make better predictions.
   - The accuracy on the training data reaches around 91-93%, while the accuracy on the validation data is consistently high, around 92-96%, indicating that the model generalizes well to unseen data.

Overall, this model seems to perform well, achieving high accuracy on both the training and validation sets. The dropout layers help prevent overfitting, and the regularization helps control the model's complexity. However, it's essential to evaluate the model's performance on unseen test data to assess its generalization ability accurately.
## Conclusions and Recommendations
Based on the analysis and models developed, here are the conclusions and recommendations:

1. **Intent Classification**:
   - The intent classification model achieved good performance, accurately categorizing user queries into predefined intent categories. This model can effectively route user queries to appropriate response handlers or workflows.

1. **Response Generation**:
   - The response generation system, utilizing cosine similarity with TF-IDF vectors, showed promising results in mapping user queries to appropriate responses. However, there is room for improvement, particularly in handling context and generating more diverse and contextually relevant responses.

1. **Model Evaluation**:
   - Model performance evaluation revealed high accuracy and generalization ability, indicating that the models can effectively handle a wide range of user queries. However, continuous monitoring and evaluation are necessary to ensure consistent performance over time.

1. **Continuous Learning and Adaptation**:
   - Implement mechanisms for continuous learning and adaptation, allowing the chatbot to evolve over time based on user feedback, new data, and changing requirements.
   - Monitor performance metrics and user satisfaction to measure the effectiveness of the chatbot and identify areas for enhancement.

By addressing these recommendations and focusing on continuous improvement, the chatbot AI system can deliver a more engaging, personalized, and effective user experience, ultimately enhancing user satisfaction and achieving the desired business outcomes.

## Deployment

This model was deployed using the following technologies:
1. __Flask__: We used flask to expose the necessary APIs needed for the chatbot like:
    - `/vectorize`: this API endpoint vectorizes the user input.
    - `/response`: this API endpoint fetches a response using __Cosine Similarity__ depending on the `tag` prediction.
2. __ReactJS__: This was used to create the front-end of the app, i.e the web UI.
3. __TensorFlow JS__: This was used to deserialize our model and enable it to be used on the front-end (this was used because `Streamlit` doesn't allow one to use a custom user-interface).
