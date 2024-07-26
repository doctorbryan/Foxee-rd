# Foxee
This project can be used for training Cuda yolov5 and TensorFlow(yet to be implimented) models. It can also run inference and model evaluation.

## requirements
1. [Node js](https://nodejs.org/en/download/)
2. Python 3.8.5


## Installation on local

### Python
Use the package manager [pip](https://pip.pypa.io/en/stable/)
```bash
cd flasklocal
pip install -r requirements.txt --user
python app.py
```
If you are using a conda environment:
```bash
conda install pywin32
```

#### Running the account management system on your local machine
```bash
cd flaskremote
pip install -r requirements.txt
python app.py
```

### Vue
Test Developement Environment: https://safe-lake-33465.herokuapp.com/#/labelling

For the test Dev env to work properly, you must run the flasklocal python app.py on your computer
```bash
cd vue
npm install
npm start
```

# Installing for yolov5 to use GPU
To install PyTorch via pip, and do have a [CUDA-capable system](https://developer.nvidia.com/cuda-gpus)

[Download Cuda](https://developer.nvidia.com/cuda-zone)

## VERIFICATION
To ensure that PyTorch was installed correctly, we can verify the installation by running sample PyTorch code. Here we will construct a randomly initialized tensor.

```python
import torch
x = torch.rand(5, 3)
print(x)
```

Additionally, to check if your GPU driver and CUDA is enabled and accessible by PyTorch, run the following commands to return whether or not the CUDA driver is enabled:
```python
import torch
torch.cuda.is_available()
```

## Deploy to Heroku
This will deploy the login server as well as the web interface to Heroku. The local flask application must run on the local machine. 
### Build
Build the vue project. This will create two folders in the **flaskremote** folder. These are used for flask to render later on in Heroku.

 - vuestatic
 - vuetemplates
```bash
npm run build
```
### Set up Heroku
https://devcenter.heroku.com/articles/getting-started-with-python

Change the git origin to your Heroku git (optional)
```bash
> git remote -v
heroku  https://git.heroku.com/foxeelogin.git (fetch)
heroku  https://git.heroku.com/foxeelogin.git (push)

> git remote set-url origin [git@your.git.repo.example.com]
```
### Deploy
```bash
cd flaskremote
git add .
git commit -m "example deploy"
git push heroku master
```

### Migrate Database
If you made changes to the DB, it needs to be updated in the Heroku Postgres DB as well.
Install postgres and make sure the /bin folder is in your system path
https://www.enterprisedb.com/downloads/postgres-postgresql-downloads
```bash
cd flaskremote
heroku pg:psql
=> (write postgresql here to update tables)
=> ALTER TABLE "Company" ADD COLUMN "CreatedDate" TIMESTAMP;
=> ALTER TABLE "Company" ALTER COLUMN "CreatedDate" SET DEFAULT now();
```
The app should be now deployed to your Heroku app. Here is the current dev environment: https://foxeelogin.herokuapp.com/app#/login
## Deploy to AWS

 1. Make a docker image
 2. Tag the image with your image like "yourdockerusername/yourappname"
 3. push to the hub
 4. go to AWS EC2
 5. https://aws.amazon.com/getting-started/hands-on/deploy-docker-containers/
