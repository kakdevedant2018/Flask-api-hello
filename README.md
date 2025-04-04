# Flask-api-hello
This project  uses Flask framework to expose an API endpoint (/hello).

## 1. Writing Flask API (main.py)

### How it works:
1. Flask App Initialise
     app = Flask (__name__) Creates a Flask application
   
3. Defining a Route
     @app.route('/hello', methods=['GET']) defines a route that listens for GET requests at /hello.
     When a GET request is received, it returns JSON

4. Running the Flask application:
     app.run(host = '0.0.0.0',port=9001)
     host = '0.0.0.0' makes the application running iside the container accesible to outside


## 2. Create a Dockerfile

It includes a information about how to build a image

1. FROM python:3.8    # Use Python 3.8 as the base image

2. WORKDIR /app       # Set the working directory inside the container

3. COPY . /app        # Copy all files from the current directory to /app inside the container

4. RUN pip install --no-cache-dir -r requirements.txt  # Install dependencies

5. EXPOSE 9001        # Declare that this container will listen on port 9001

6. CMD ["python3", "main.py"]  # Command to start the Flask app

## 3. Building a Docker Image

docker build -t flask-app .

1. docker build → Creates a new Docker image.

2. -t flask-app → Tags the image as flask-app.

3. . → Uses the current directory (where the Dockerfile is located).


### What Happens on running above command:

1. Docker downloads Python 3.8.

2. It copies your files into the container.

3. It installs Flask (pip install -r requirements.txt).

4. It prepares the container to run your app.

Now the docker image is created

## 4. Running the Flask App in Docker

docker run -p 9001:9001 flask-app

docker run → Runs a new container.
-p 9001:9001 → Maps port 9001 on your machine to port 9001 inside the container.
flask-app → Runs the image you built.


## 5. Check if the API is working or not

Through curl command or through web brower as this a only GET request

curl -X GET http://localhost:9001/hello

