
# Setup for Python:

1. Install Python (Setup instructions)

2. Install Python packages

pip3 install -r training/requirements.txt
pip3 install -r api/requirements.txt

3. Install Tensorflow Serving (Setup instructions)

# Setup for ReactJS

Install Nodejs (Setup instructions)
Install NPM (Setup instructions)
Install dependencies
cd frontend
npm install --from-lock-json
npm audit fix
Copy .env.example as .env.

# Change API url in .env.

Setup for React-Native app
Go to the React Native environment setup, then select React Native CLI Quickstart tab.

# Install dependencies

cd mobile-app
yarn install
2.1 Only for mac users
cd ios && pod install && cd ../
Copy .env.example as .env.

Change API url in .env.

# Training the Model

Download the data from kaggle.
Only keep folders related to Potatoes.
Run Jupyter Notebook in Browser.
jupyter notebook
Open training/potato-disease-training.ipynb in Jupyter Notebook.
In cell #2, update the path to dataset.
Run all the Cells one by one.
Copy the model generated and save it with the version number in the models folder.

# Running the API

Using FastAPI
Get inside api folder
cd api
Run the FastAPI Server using uvicorn
uvicorn main:app --reload --host 0.0.0.0
Your API is now running at 0.0.0.0:8000

# Using FastAPI & TF Serve

Get inside api folder
cd api
Copy the models.config.example as models.config and update the paths in file.
Run the TF Serve (Update config file path below)
docker run -t --rm -p 8501:8501 -v C:/Code/potato-disease-classification:/potato-disease-classification tensorflow/serving --rest_api_port=8501 --model_config_file=/potato-disease-classification/models.config
Run the FastAPI Server using uvicorn For this you can directly run it from your main.py or main-tf-serving.py using pycharm run option (as shown in the video tutorial) OR you can run it from command prompt as shown below,
uvicorn main-tf-serving:app --reload --host 0.0.0.0
Your API is now running at 0.0.0.0:8000

# Running the Frontend

Get inside api folder
cd frontend
Copy the .env.example as .env and update REACT_APP_API_URL to API URL if needed.
Run the frontend
npm run start

# Running the app

Get inside mobile-app folder
cd mobile-app
Copy the .env.example as .env and update URL to API URL if needed.

Run the app (android/iOS)

npm run android
or

npm run ios
Creating public (signed APK)

# Creating the TF Lite Model

Run Jupyter Notebook in Browser.
jupyter notebook
Open training/tf-lite-converter.ipynb in Jupyter Notebook.
In cell #2, update the path to dataset.
Run all the Cells one by one.
Model would be saved in tf-lite-models folder.

# Deploying the TF Lite on GCP

Create a GCP account.
Create a Project on GCP (Keep note of the project id).
Create a GCP bucket.
Upload the potatoes.h5 model in the bucket in the path models/potatos.h5.
Install Google Cloud SDK (Setup instructions).
Authenticate with Google Cloud SDK.
gcloud auth login
Run the deployment script.
cd gcp
gcloud functions deploy predict_lite --runtime python38 --trigger-http --memory 512 --project project_id
Your model is now deployed.
Use Postman to test the GCF using the Trigger URL.
Inspiration: https://cloud.google.com/blog/products/ai-machine-learning/how-to-serve-deep-learning-models-using-tensorflow-2-0-with-cloud-functions

# Deploying the TF Model (.h5) on GCP

Create a GCP account.
Create a Project on GCP (Keep note of the project id).
Create a GCP bucket.
Upload the tf .h5 model generate in the bucket in the path models/potato-model.h5.
Install Google Cloud SDK (Setup instructions).
Authenticate with Google Cloud SDK.
gcloud auth login
Run the deployment script.
cd gcp
gcloud functions deploy predict --runtime python38 --trigger-http --memory 512 --project project_id
Your model is now deployed.
Use Postman to test the GCF using the Trigger URL.
Inspiration: https://cloud.google.com/blog/products/ai-machine-learning/how-to-serve-deep-learning-models-using-tensorflow-2-0-with-cloud-functions
