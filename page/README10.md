Step 1: Open Ubuntu Terminal
Create a project folder:

mkdir mlflow_experiment
cd mlflow_experiment


Check Python and pip:

python3 --version
pip3 --version


Step 2: Create a virtual environment:

python3 -m venv venv
source venv/bin/activate


Step 3: Install required libraries:

pip install mlflow scikit-learn pandas


Check MLflow:

mlflow --version


Step 4: Start the MLflow server
Open a second terminal and enter:

cd ~/mlflow_experiment
source venv/bin/activate
mlflow server --port 5000


Keep this terminal open.
Step 5: Open MLflow in the browser
Open Firefox or Chrome and enter:

http://localhost:5000
Step 6: Create the training file
Return to the first terminal and enter:
nano train_model.py


Paste this simple training code:

import mlflow
import mlflow.sklearn
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import accuracy_score

mlflow.set_tracking_uri("http://localhost:5000")
mlflow.set_experiment("Iris_ML_Lifecycle")

iris = load_iris()
X = iris.data
y = iris.target

X_train, X_test, y_train, y_test = train_test_split(
    X, y, test_size=0.2, random_state=42
)

model = LogisticRegression(max_iter=200)
model.fit(X_train, y_train)

prediction = model.predict(X_test)
accuracy = accuracy_score(y_test, prediction)

with mlflow.start_run() as run:
    mlflow.log_param("algorithm", "Logistic Regression")
    mlflow.log_metric("accuracy", accuracy)

    mlflow.sklearn.log_model(
        sk_model=model,
        name="iris_model",
        registered_model_name="Iris_Logistic_Regression"
    )

    print("Training completed")
    print("Accuracy:", accuracy)
    print("Run ID:", run.info.run_id)



Save the file:
1. Press Ctrl + O.
2. Press Enter.
3. Press Ctrl + X.
Step 7: Run the training program
In the first terminal, enter:

python train_model.py


The program trains the model and displays the accuracy and Run ID.
Step 8: Check MLflow
In your browser at http://localhost:5000:
1. Open Iris_ML_Lifecycle.
2. Click the experiment run.
3. Check the accuracy.
4. Check the registered model Iris_Logistic_Regression.
Step 9: Create the prediction file
In the first terminal:

nano predict.py


Paste this code:

import mlflow

mlflow.set_tracking_uri("http://localhost:5000")

model = mlflow.pyfunc.load_model(
    "models:/Iris_Logistic_Regression/1"
)

prediction = model.predict([[5.1, 3.5, 1.4, 0.2]])

print("Prediction:", prediction)



Save with Ctrl + O, press Enter, then Ctrl + X.
Step 10: Run the prediction program:

python predict.py


Expected output:
Prediction: [0]


Here, 0 represents the Iris Setosa flower.
Step 11: Deploy the model
Open a third terminal:

cd ~/mlflow_experiment
source venv/bin/activate


Start the model server:

mlflow models serve \
-m "models:/Iris_Logistic_Regression/1" \
-p 5001


Keep this terminal open.
Step 12: Test the deployed model
Open a fourth terminal and enter:

curl -X POST http://127.0.0.1:5001/invocations \
-H "Content-Type: application/json" \
-d '{"inputs": [[5.1, 3.5, 1.4, 0.2]]}'


The response should contain prediction 0.