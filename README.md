# Estimating Cosmological Parameters with an Artificial Neural Network

![universe-11636_960_720-1-800x540](https://github.com/user-attachments/assets/e6b39f4a-c540-4d63-ba5b-4bc178321112)


### Introduction:

**Goal:** Develop a neural network model to estimate $\Omega_{matter}$ (dark matter density parameter) and the Hubble constant ($H_0$) by analyzing the relationship between Hubble values and redshift (z).

**Data Generation:**

* **Friedmann Equation:**
  

 $H(z) = H_0 \cdot \sqrt{\Omega_m \cdot (1 + z)^3 + \Omega_\Lambda}$

* **Assumptions:**
  * Radiation density parameter ($\Omega_r$) is assumed to be 0.
  * $\Omega_\Lambda = 1 - \Omega_m$
* **Data Generation Process:**
  * Generate synthetic data for Hubble values using the Friedmann equation.
  * Add noise to the data based on residuals from observational versus theoretical values.
  * Vary Hubble constant $H_0$, $\Omega_m$ across a range of possible values to create a comprehensive dataset.
 
  ![download](https://github.com/user-attachments/assets/7776b7c0-66c5-48a7-b636-78a366bb5d8b)




### Data Preparation and Neural Network Training

#### Splitting the Data
To prepare the data for training, we first extract the features and labels:
- `X`: The input features consisting of redshift values and generated Hubble values.
- `y`: The target labels, which include the Hubble constant (($H_0$)), ($\Omega_m$) parameters.

We normalize the input features using `MinMaxScaler`, ensuring that all values are scaled between 0 and 1 to improve the convergence of the neural network. The data is then split into training and testing sets, with 20% of the data reserved for testing, using the `train_test_split` function from `sklearn`. This ensures that the model can be evaluated on unseen data.


#### Neural Network Architecture
We define a sequential neural network model using the `TensorFlow` and `Keras` libraries. The model is designed to predict the Hubble constant and ($\Omega_m$) simultaneously from the redshift and Hubble values. Key elements of the architecture include:
- Input layer: It takes the normalized feature set.
- Hidden layers: Three densely connected hidden layers with `ReLU` activation functions, followed by a `Dropout` layer to prevent overfitting by randomly turning off 20% of neurons during training.
- Output layer: The output consists of two neurons predicting the Hubble constant and \($\Omega_m\$).

The network is compiled using the Adam optimizer with a mean squared error (MSE) loss function, suitable for regression tasks.

![Design](https://github.com/user-attachments/assets/1a49274a-d6af-4c16-b213-611d1a2e6fed)


####  Training the Neural Network

We train the model over 100 epochs using a batch size of 64. To enhance the model's performance and reduce overfitting, we use a callback (`ReduceLROnPlateau`) that reduces the learning rate by a factor of 0.5 if the validation loss plateaus. This prevents the model from getting stuck in local minima. A portion (20%) of the training data is used for validation during the training process to monitor the model’s performance.


####  Model Evaluation and Visualization

After training, the model is evaluated on the test set to determine the test loss (MSE). We also plot the training and validation loss over the epochs to observe the model's learning curve, ensuring that the model has not overfitted to the training data.

![Figure_1](https://github.com/user-attachments/assets/d7513b80-a55a-4ea5-bb71-e8f64e0a902b)


#### Predicting with Uncertainty (Monte Carlo Dropout)

To incorporate uncertainty into the predictions, we utilize Monte Carlo Dropout, where we perform multiple forward passes (100 iterations) through the model with dropout enabled. This method allows us to estimate both the mean and standard deviation of the predictions, giving insights into the uncertainty of the model's predictions.

![download (1)](https://github.com/user-attachments/assets/cb361161-cdc9-4bb0-b139-2e47b81ea64c)

### Future Work

Our simple Neural Network shows the tendency to predict the Cosmological parameters to high accuracy. Nevertheless, It’s not uncommon to encounter performance issues with a neural network, especially when dealing with complex problems like cosmological parameter estimation (Hubble constant, Omega values) from redshift data. The challenge could stem from both the complexity of the problem and potential issues with the model or data. Let's break this down:

1. Problem Complexity
Cosmological Models: Estimating parameters like the Hubble constant and Omega values involves fitting complex nonlinear models. Even small changes in these parameters can lead to large differences in the predicted Hubble values due to the underlying equations (e.g., Friedmann equations).

2. Degeneracy: Some parameters may be highly correlated or degenerate. For instance, different combinations of Omega_m and Omega_Lambda could produce similar Hubble values for certain redshift ranges, making it hard for the model to distinguish between them.

3.  Advanced Techniques: Bayesian Neural Networks (BNNs)
BNNs could help by quantifying the uncertainty in predictions, which is particularly important in cosmology where error bounds on parameters are essential.
