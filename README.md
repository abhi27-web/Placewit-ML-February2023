# Placewit-ML-February2023

## CLASS 1 : 26 February 2023

#### Session 1
- Introduction to Python Programming
- Introduction to the Kaggle Platform(https://www.kaggle.com/)
- Python Fundamentals

#### Session 2
- Basic Python Libraries
- Pandas
- Numpy
- Matplotlib
- Seaborn (Basic intro)
- EDA using 4 Key Libraries on Titatnic Dataset


## CLASS 2 : 5 March 2023

#### Session 1
- Data Visualizations Basics using Matplotlib
- Line Chart
- Scatter Plot
- Barplot
- Piechart

#### Session 2
- Working on Complex EDA	
- Multiple attribute graphs
	Titanic EDA Answers

## CLASS 3 : 12 March 2023

#### Session 1
- Introduction to Machine Learning	
- Machine Learning:History and Origin
- Supervised and Unsupervised Algorithms
- Clustering
- Classification and Regression

#### Session 2
- Linear Regression	
- Introduction to Linear Regression
- Gradient Descent
- Cost Function
- Linear Regression Algorithm from Scratch

## CLASS 4 : 19 March 2023

#### Session 1
- Regression Metrics
- RMSE
- MSE
- MAE
- Confusion Matrix
- Sklearn Linear regression 

#### Session 2
- Dataset Preprocessing
- Dealing with categorical Variables
- Applying LR on House Price data

## CLASS 5 : 26 March 2023

#### Session 1
- Logistic Regression

#### Session 2
- Logistic Regression code from Scratch
- Application of Logistic Regression

## CLASS 6 : 2 April 2023

#### Session 1
- Decision Tree from Scratch

#### Session 2
- Decision tree using sklearn application
- Grid Search Hyperparameter Tuning

## CLASS 7 : 9 April 2023

#### Session 1
- Random Forest from Scratch
- Random Forest using Sklearn

#### Session 2
- Random Forest Application
- KNN from Scratch + Application

## CLASS 8 : 16 April 2023

#### Session 1
- Working on Text Data
- Data Cleaning

#### Session 2
- Data Vectorization
- Application on a dataset

## CLASS 9 : 23 April 2023

#### Session 1
- Basics of NN
- Transfer Learning
- How does NN work

#### Session 2
- Basic idea behind Backpropogation
- Coding a basic NN

## CLASS 10 : 12 May 2023 and 14 May 2023

#### Session 1
- Backpropogation: Optimizing 3 values simultaneously
- Optimizing all the Values Simultaneously

#### Session 2
- NN Part 3: ReLU
- NN Part 4: Multiple Inputs and Outputs

## CLASS 11 : 14 May 2023

#### Session 1
- RNN


```yaml
data_config:
  source:
    type: "hf"
    repo_id: "datasets-examples/doc-image-1"
    split: "train"
    streaming: true

  sink:
    type: "hf"
    repo_id: <repo_name>
    config_name: MM-doc-image-1
    split: train
    push_to_hub: true
    private: true
    token: <hf_token>

graph_config:
  nodes:
    judge_pokemon:
      output_keys: pokemon
      node_type: llm
      prompt:
        - user:
            - type: text
              text: |
                Identify the pokemon in the provided image.
            - type: image_url
              image_url: "{image}"

      model:
        name: gpt-4o
        parameters:
          max_tokens: 1000
          temperature: 0.3
  edges:
    - from: START
      to: judge_pokemon
    - from: judge_pokemon
      to: END

output_config:
    output_map:
        id:
          from: "id"
        image:
          from: "image"
        pokemon:
          from: "pokemon"
```
