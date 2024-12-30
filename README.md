# XGBoost-from-scratch
Here you can find an explanation of eXtreme Gradient Boosting (XGB) for scratch and its realization without ML libs.

1)Core Idea of the Algorithm

Gradient Boosting builds a model by combining weak learners (typically decision trees) sequentially, where each subsequent model learns to correct the residual errors of the previous ones. The process minimizes a predefined loss function (e.g., Mean Squared Error, MSE) using gradient descent.

2)Objective Function:

For regression problems, the loss function is typically the Mean Squared Error (MSE)

<img width="232" alt="Screenshot 2024-12-29 at 7 22 08 pm" src="https://github.com/user-attachments/assets/9eb08804-0432-4b3c-9352-f48121806434" />

where 

𝑦𝑖 is the true value of the target variable for the object 

𝑦^ - model prediction.

