1. Problem Definition
   
The goal of XGBoost is to minimize prediction error by sequentially adding weak models (e.g., decision trees), each of which corrects the residuals of the previous models.

2. Loss Function
   
For regression tasks, the Mean Squared Error (MSE) is used as the loss function:

![Screenshot 2024-12-30 at 1 08 33 pm](https://github.com/user-attachments/assets/d78e2365-aded-4369-b5ac-e512e7dc57b3)

Example: Suppose 
𝑦=[10,15,20]  and the initial predictions are 𝑦^=[12,15,18] 


![Screenshot 2024-12-30 at 1 10 15 pm](https://github.com/user-attachments/assets/6a9b5acc-1daf-4282-b680-95537e377753)

3. Initial Prediction
   
The initial prediction is the mean of the target variable:

![Screenshot 2024-12-30 at 1 10 47 pm](https://github.com/user-attachments/assets/d98a2d1e-3cfb-462b-81eb-4f3b14ddd768)

Example: If 𝑦=[10,15,20]  , then:

![Screenshot 2024-12-30 at 1 11 21 pm](https://github.com/user-attachments/assets/d6a2ff2c-9c29-48a7-9202-67963153a1a3)

This serves as the baseline prediction.

4. Gradient
   
What is a gradient?
The gradient indicates how to adjust the current predictions to reduce the loss. It is the first derivative of the loss function with respect to the predicted value.

How is the gradient calculated for MSE?
The loss function is:

![Screenshot 2024-12-30 at 1 37 59 pm](https://github.com/user-attachments/assets/6eb68f2b-e248-46fe-808b-5080f16f5870)

Taking the partial derivative with respect to  𝑦^𝑖 

∂𝐿/∂𝑦 = −2(𝑦𝑖−𝑦^𝑖)

The gradient is the difference between the true value and the current prediction, multiplied by -2.

Example: 

For  𝑦=[10,15,20] and y^ =[12,15,18]:

g1 =−2(10−12)=−2⋅(−2)=4
g2 =−2(15−15)=0
g3 =−2(20−18)=−4
The gradients are:

g = [4,0,−4]


5. Hessian

What is a Hessian?
The Hessian describes how the gradient changes as predictions are updated. It is the second derivative of the loss function with respect to 
𝑦^𝑖

How is the Hessian calculated for MSE?
The gradient:  ∂𝐿/∂𝑦 = −2(𝑦𝑖−𝑦^𝑖)

Taking the second derivative hessian equals 2

Why is the Hessian constant?
For MSE, the second derivative does not depend on 𝑦𝑖 or 𝑦^𝑖. It is constant because the equation is quadratic.

6. Tree Building: Finding Splits
   
How does splitting work?
The algorithm finds the split point that maximizes the information gain.

Gain Formula:

![Screenshot 2024-12-30 at 1 46 22 pm](https://github.com/user-attachments/assets/7a085bd7-bbea-4279-9994-13afa6a7db7c)


Example: Suppose we have a feature 
x=[1,2,3], corresponding to  y=[10,15,20], and gradients  g=[4,0,−4].

Consider splitting at  x≤2 (left: [1,2], right: [3])

Left branch:
G left = 4 + 0 = 4 , H left = 2 + 2 = 4

Right branch:

G right = −4  , H right = 2 


Overall:
G total = 4 + (-4) = 0
H total = 4 + 2 = 6

Calculate Gain:

<img width="384" alt="Screenshot 2024-12-30 at 9 30 54 pm" src="https://github.com/user-attachments/assets/d58e30c4-b34d-4f79-aef3-158676453376" />


7. Updating Leaf Weights
After finding the optimal split, the leaf weights (predictions) are updated using the formula:

<img width="187" alt="Screenshot 2024-12-30 at 9 32 17 pm" src="https://github.com/user-attachments/assets/a446a790-5f75-47e2-855d-f78b239005df" />

Example:

For ther left branch with λ = 1, w = -4 / (4+1) = -0.8


8. Updating Predictions
Predictions are updated as follows:

<img width="200" alt="Screenshot 2024-12-30 at 9 33 54 pm" src="https://github.com/user-attachments/assets/0cab36d9-8922-4e1e-90bf-58819d02dccd" />

Example:

If 𝑦^ = =[15,15,15] and the new weight left  =−0.8 for the first leaf:

𝑦^1 new = 15 + 0.1 * (-0.8) = 14.92


9. Iteration
This process is repeated: new gradients are calculated, trees are built, and predictions are adjusted. With each iteration, the Mean Squared Error (MSE) decreases.

Final Model
The final model is an ensemble of all the trees:

<img width="168" alt="Screenshot 2024-12-30 at 9 36 06 pm" src="https://github.com/user-attachments/assets/39a6b2e1-4a81-4f2c-9999-76f1bc5562b7" />





