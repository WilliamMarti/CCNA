
Uses computer to simulate intelligence, allowing them to exhibit behaviors typically associates with humans, such as recognizing patterns, learning, making decisions, and solving problems.  

Examples:
- Virtual assistances.  Siri, Alexa, Google assistants
- Recommendation Systems.  Netflix, Youtube, Amazon
- Self-Driving Cars.  Tesla Waymo
- Chatbots.  ChatGPT, virtual concierges
- Gameplay.  Stockfish.  AlphaGo

**Machine Learning** - Subnetof AI that focuses on enabling computers to learn from data and improve without the need for explicit programing

Input Data -> Model Learns from Data Patterns -> Make predictions on new data

Machine Learning is a subset of AI

Examples:
- Email Spam Filtering
- Personalized Product recommendations
- Fraud Detection
- Natural Language Processing(NLP)

##### Types of ML

**Supervised Learning** - Model trained on labeled data.  Correct answers are provided to make predictions or classifications on new data

**Unsupervised Learning** - Model given unlabeled data and is tasked with finding patterns, relationships, or group within the data

**Reinforcement Learning** - Model learns by interacting with an environment, receiving rewards or penalties based on its actions to max its performance over time.  

**Deep Learning** - Specialized subnet of ML that uses multi-layered neural networks to handle large datasets and perform complex tasks like image recognition and natural language processing.

**Supervised Learning** - 
- Trains model on labeled dataset
- Each input provided to the model has corresponding label
- By examining the label examples the model learns to the relatoionship between the data and the given label
- By Training on labeled examples, the model learns to classify view unlabeld data with the high accuracy


| Advantanges                                    | Disadvantages                                                                        |
| ---------------------------------------------- | ------------------------------------------------------------------------------------ |
| Highly accurate when labeled data is available | Requires large labeled data sets which can be expensive and time consuming to create |
| Straightforward to understand and implement    | Output is limited to the labels in the training data                                 |

**Unsupervised Learning*** - 
No predefined label provided

Model can discover patterns, structures, or relationships within data
	Groups (Clusters) similar data points based on shared features


| Advantanges              | Disadvantages                                          |
| ------------------------ | ------------------------------------------------------ |
| No need for labeled data | Interpretation and labeling of the results is required |
| Reveal hidden patterns   | Less Accurate                                          |

**Reinforcement Learning** -

Train by rewarding or penalizing its action in a given environment to maximize its performance over time

Model (called an Agent) interacts with environment
Takes action and receives feedback
Agent used feedback to learn which actions leads to best results

Self-Driving - Navigate safely by trial and error
Game AI - Master strategies in games like Chess or Go
Robotics - Teach robots how to walk, pick up objects, perform tasks

| Advantanges                           | Disadvantages                                                         |
| ------------------------------------- | --------------------------------------------------------------------- |
| Capable of learning complex behaviors | Resource intensisve                                                   |
| Adapts to dynamic environments        | Risk of sub-optimal learning if reward system isn't designed properly |
##### Deep Learning

Uses Artificial Neural Networks to process and learn from large and complex datasets

Inspired by how biological neural networks like the human brain process information

Data is processed through multiple layers of nodes(neurons) with each layer extracting increasingly abstract features

Can be trained using supervised, unsupervised, and/or reinforcement methods

| Advantanges                                                                                       | Disadvantages                                                                               |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| Excels at handling larger unstructed data sets like images/audio/text                             | Resource intensive                                                                          |
| Archives state-of-the-art performance n tasks like image recognition, NLP, and autonomous driving | Model can be "black box" making it difficult to interpret how it arrives at its destination |

##### Predictive and Generation AI

**Predictive AI** - Use machine learning AI to analyze historical data and predict future outcomes or trends
	Security anomaly detection, weather forecasting

**Generative AI** - Use machine learning to learn patterns from existing data and create new content, such as text, images, or audio. 
	ChatGPT, Gemini, Midjourney, DALL-E

**Predictive AI** - Analyze historical data to forecast future outcomes, trends.

Model identifies patterns and correlations in past data.  

Learned patterns are applied to make predictions

Applications:
- Healthcare - Predict patient outcomes
- NetSec - Detect anomalies that might indicate a potential threat or failure
- Traffic Management - Predicting congestion based on historical and real-time traffic data

| Advantanges                                               | Disadvantages                                                                      |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Improves decision making by providing actionable insights | Requires high quality, relevant historical data                                    |
| Dtects potential problems before they occur               | Accuracy depends on how well the patterns in past data generalize to new scenarios |
##### Generative AI

Learns patterns from existing data and creates new content such as text, images, and audio

Focuses on producing outputs that resemble the input that it was trained on

Applications:
- Text Generation - ChatGPT, Gemini, Copilot
- Image Generation - Midjourney, DALL-E
- Video Generation - Sora(OpenAI), Veo2(Google)

| Advantanges                                                    | Disadvantages                                                             |
| -------------------------------------------------------------- | ------------------------------------------------------------------------- |
| Great for tasks where human input is limited or time consuming | Risk of misuse(Deepfakes, plagarism)                                      |
| Enabled automation of content creation                         | Generated content is only as good as the quality of the training material |
|                                                                | Hallucinations                                                            |

