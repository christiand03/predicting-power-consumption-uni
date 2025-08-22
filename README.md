# Predicting Power Consumption using Machine Learning
This is a two person group project I did for the Course "Introduction to Deep Learning and AI in Python" at TU Dresden to showcase a complete Machine Learning Pipeline. It aims to predict the hourly power consumption using historical factory data. Additionally external weather impacts are taken into account. The project combines classical machine learning and deep learning techniques. The company data was provided by Infineon Dresden.

## Overview
- **Goal**: Forecast the hourly power consumption for the next 72 hours based on factory output and the weather situation.
- **Models Used**: Random Forest Regressor meant to serve as a baseline and a Neural Network implemented in Tensorflow.
- **Data Sources**: Anonymized factory data from Infineon Dresden combined with local weather data.
- **Business Relevance**: Helps identify consumption patterns to improve energy planning and therefore reduce costly consumption spikes.

## Technologies Used

| Category             | Tools & Libraries                        |
|----------------------|-------------------------------------------|
| Language             | Python                                    |
| Data Handling        | pandas, NumPy                             |
| Visualization        | matplotlib                                |
| Machine Learning     | scikit-learn (RF Regressor, Grid Search)  |
| Deep Learning        | Tensorflow                                |
| Model Evaluation     | RMSE, R² Score                            |

## Approach

1. **Data Preparation**
   - Integrated factory data with external weather sources.
   - As the data was provided solely for the project only minimal cleaning was needed.
   - Splitting data into training and testing sets.

2. **Baseline Model**
   - Trained a **Random Forest Regressor** to establish a benchmark.
   - Evaluated using RMSE and R².

3. **Neural Network Models**
   - Built two conventional 3-layer feedforward neural networks using Tensorflow (one for factory output, one for power consumption).
   - Two Models are needed as the power consumption is dependant on factory output which was not provided after the cutoff date.
   - Optimized using the Nadam optimizer.
   - Evaluated using RMSE and R².
  
4. **Grid Search**
   - Used to find optimal hyperparameters to increase performance
  
5. **Visualization of Results**
   - Displayed below under Conclusion & Visualization.

## Results

Performed on Test Dataset:
| Model                              | RMSE (↓)  | R² Score (↑) |
|------------------------------------|-----------|--------------|
| Random Forest (Factory Output)     | 3.428e-05 | 0.9989       |
| Random Forest (Power Consumption)  | 7.007e-04 | 0.9732       |
| Neural Network (Factory Output)    | 0.0196    | 0.9888       |
| Neural Network (Power Consumption) | 0.0354    | 0.9523       |

The results are unusually strong. This is due to the fact that the data was randomly shuffled for training and testing, which is a practice that is not appropriate for time series data, but was unknown to us at the time.
Another potential improvement would be to use a recurrent neural network, such as an LSTM, instead of a simple sequential model.
However, the primary goal of this project was to gain experience working with a machine learning pipeline rather than achieving perfect results on the first attempt. These refinements were insights I only gained more than a year later from another course.

## **Conclusion & Visualizations**

![image](https://github.com/user-attachments/assets/da167d0d-5102-4070-af2b-6997f52571cb)

Plotting the Predictions from the Regression Model and the Neural Network shows a striking simmilarity between the two. The Power Consumption Curves are very simmilar and follow the same pattern. The Neural Network has slightly more volatile Factory Output Predictions but are overall not far apart. Interestingly the Neural Network predicts the exact opposite trend from the Regression Model for the Factory Output on the third day. Given that both Models predict a simmilar Power Consumption Curve we are certain that both models interpret the underlying data in a simmilar way. Therefore we are not sure what is causing this mirroring effect.

![image](https://github.com/user-attachments/assets/55560b67-d928-4b10-97ff-2b1e5d9f9d3e)

These are the last 72 hours before we begin our Prediction. Our Models both predict a drop in Factory Output of around 10% directly after the last datapoint. Given that both models predict nearly the same value, we are not concerned that this 10% drop is unreasonable. Given that we were not meant to know what these anonymized values represent in reality.
Both our models predict less Power Consumption and also less volatility. We predict no Power Consumption Spikes for the next three days, unlike the Spike that can be seen in the Plot above.



