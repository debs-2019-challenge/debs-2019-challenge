# DEBS 2019 Grand Challenge

This repository provides a sample HTTP-client to demonstrate how to integrate your solution for participation in the DEBS Grand Challenge's 2019 edition.

You can use this repository as a jump start/template for your solution. Note, the example is written in Python. However, you can use any language to provide your solution
as long as it is communicates through the HTTP/REST interface of the benchmark system.

For local testing, we provide you with Docker Compose setup to reduce the complexity of integration with the Benchmark System.
Please read the instructions below in order to get an insight how you can get started.

## About this repository

This repository contains the following project structure:
* `dataset` folder should contain your training datasets `in.csv` and `out.csv`.
* `client_app` folder for an example http-client.
* `docker-compose.yml` - defines the services to run the benchmark locally.
* `Dockerfile.client` - defines the steps needed to build container with your prediction system (if you decided to use another language than Python, you will need create your own Docker image).

## Before you start

Make sure you have Docker Engine and Docker Compose installed.
You may use the official link below for downloading:
[Download Docker Engine](https://docs.docker.com/get-started/#prepare-your-docker-environment
https://docs.docker.com/compose/install/#install-compose)

Check your installation:
```
  $ docker --version
  $ docker-compose --version
```

## How to get started

You need to implement your solution as a HTTP-client. An example HTTP-client written in Python is provided in `/client_app` folder.
You may use this code as it is, we already implemented all basic functionality that you may need. Just plug in your prediction and you are ready to submit your solution.
However you are free to use any language that suits your needs.

1. Clone this repository
2. Place your `out.csv` and `in.csv` files in `/dataset` folder for the Benchmark System Container to be able to test your prediction accuracy and latency.
3. Implement your solution as REST-based HTTP-client that issues the appropriate GET and POST requests (you may see an example implementation in `client_app.py`).
4. The http client should connect to the host specified in the `BENCHMARK_SYSTEM_URL` environemnt variable.


| Method     | URI                               | Action                                                            |
|------------|-----------------------------------|-------------------------------------------------------------------|
| `GET`      | `scene`                           | `retrieves a new scene - list of coordinates with timestamps`     |
| `POST`     | `scene`                           | `submit the prediction result for the previously retrieved scene` |

5. Add your dependencies to `Dockerfile.client`. If you use Python, check `line 12` of this file, and do not forget to add dependencies that your client program uses.
6. To start the evaluation of your solution run:
      ```
      $ docker-compose up
      ```
7. Check the logs of `'benchmark-server'` Docker container to see details of your run.
    Use this command:
      ```
      $ docker logs benchmark-system
      ```
8. Make changes to your system if needed.
After any change to your prediction system or HTTP-client, please run these commands:
      ```
      $ docker-compose down
      ```
    This will stop the previous run of benchmark system. Then run:
      ```
      $ docker-compose up --build
      ```
    To rebuild with changes you made.
    
  ## Questions & Answers
  Please use the issue tracker for any questions, issues concerning the provided data set as well as integration & implementation.
