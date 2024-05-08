# Ex.No: 13 Learning – Use Supervised Learning  

### DATE: 07/05/2024                                                                           

### REGISTER NUMBER : 212221040002

### AIM: 
To write a program to train the classifier for diabeties.

###  Algorithm:
Step 1: Load the diabetes dataset.
Step 2: Split the dataset into features (input) and target variable (output).
Step 3: Split the data into training and testing sets.
Step 4: Scale the features using StandardScaler.
Step 5: Train a neural network classifier on the training data.
Step 6: Evaluate the classifier's accuracy on both training and testing data.
Step 7: Create a function to predict diabetes based on user input.
Step 8: Launch a Gradio interface for users to input their data and get a prediction.
Step 9: Stop the program.

### Program:
```
#import packages
import numpy as np
import pandas as pd
import gradio as gr
import pandas as pd
data = pd.read_csv('diabetes.csv')
data.head()
x = data.drop(['Outcome'], axis=1)
y = data['Outcome']
print(x[:5])

from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test= train_test_split(x,y)

#scale data
from sklearn.preprocessing import StandardScaler
scaler = StandardScaler()
x_train_scaled = scaler.fit_transform(x_train)
x_test_scaled = scaler.fit_transform(x_test)

#instatiate model
from sklearn.neural_network import MLPClassifier
model = MLPClassifier(max_iter=1000, alpha=1)
model.fit(x_train, y_train)
print("Model Accuracy on training set:", model.score(x_train, y_train))
print("Model Accuracy on Test Set:", model.score(x_test, y_test))

#create a function for gradio
def diabetes(Pregnancies, Glucose, Blood_Pressure, SkinThickness, Insulin, BMI,Diabetes_Pedigree, Age):
    x = np.array([Pregnancies,Glucose,Blood_Pressure,SkinThickness,Insulin,BMI,Diabetes_Pedigree,Age])
    prediction = model.predict(x.reshape(1, -1))
    if(prediction==0):
      return "NO"
    else:
      return "YES"

outputs = gr.Textbox()
app = gr.Interface(fn=diabetes, inputs=['number','number','number','number','number','number','number','number'], outputs=outputs,description="Detection of Diabeties")
app.launch(share=True)
```

### Output:
![image](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/f65f8935-6a7a-4259-80d1-9ad3f507c81a)
![image](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/afa24ae2-4f97-4a7a-b291-0c63aa878612)
![280472576-361414a1-d8fa-4fe0-a7b7-6cfc96201742](https://github.com/NithishThirumalai/AI_Lab_2023-24/assets/114301782/d907f1f6-49ff-41c9-95c1-09d90122ee41)


### Result:
Thus the system was trained successfully and the prediction was carried out.
