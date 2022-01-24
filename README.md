# license-scan
Web application leveraging rekogntion, lambda, and S3 to scan face images and return pertinent information. This version only supports face scans but a later version can include text detection to pull information such as name, DoB, etc from the license. 

# Setup Steps

## Setup IDE
- Open up the code in your favorite IDE
- Create a venv in your IDE
- install the dependencies in your requirements.txt file using the “pip install -r requirements.txt”

## Setup AWS Env
- Create an S3 bucket, then create a folder in that bucket which all the images will be uploaded to
- Create a dynamoDB table with “pic_id” as the partition key, keep the type as a String
- Run “python create_collection.py”
  - Note down the collection ID you used
- Copy this collection ID and DynamoDB table name into the lambda.py file
- Create a lambda function with the code written in the “lambda.py” file and runtime of python 3.9
- Create an “S3 object created” trigger for that lambda; remember to add a prefix because your S3 bucket has a folder in it that holds those images
- Update permissions for created role (for development just give that role admin permissions)
- Deploy the lambda function

## Set up Flask App
- Update the “app.py” file with the bucket, folder, and DynamoDB table name
- Run “python app.py” to start the flask app

## Using App
- Navigate to the URL and upload a picture
  - Its immportant that the picture doesnt have any "/" in the name. Best to rename it to something will hyphens ("-") or underscores ("_"). For example rename "this/picture" to "this-picture" or "this_picture"
- Wait a few seconds as the process takes place and click on the display tab to view the results
