[![Recommend top N movies from Model prediction with DNN](https://github.com/asheshd/MLOps-IISc-Proj-UI/actions/workflows/predict_movies.yaml/badge.svg?branch=main)](https://github.com/asheshd/MLOps-IISc-Proj-UI/actions/workflows/predict_movies.yaml) [![Train Movie Recommender Model with DNN](https://github.com/asheshd/MLOps-IISc-Movie_Recommender/actions/workflows/model_train.yaml/badge.svg?branch=main)](https://github.com/asheshd/MLOps-IISc-Movie_Recommender/actions/workflows/model_train.yaml)

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <a href="https://github.com/asheshd/MLOps-IISc-Movie_Recommender">
    <img src="images/logo.png" alt="Logo" width="80" height="80">
  </a>

<h2 align="center"> Recommendation System MLOps Project with Deep Learning for IISc</h2>

  <p align="center">
  With extensive growth and innovation in Data Science it has become critical to employ practices that enhance efficiency and robustness of the entire development and execution process. Machine learning systems come with special challenges in this regard compared to traditional practices like Agile and DevOps, thereby leading to MLOps. One such class of ML models that can illustrate the efficacy of MLOps are recommendation systems. Recommendation systems provides suggestions that best suit the users' needs by offering personalized content based on past behavior. They are used in various fields such as retail, advertising, recommendation of movies, songs, etc. This project first implements a recommendation system for movies using the MovieLens 100k database based on a collaborative filtering method and then establishes it in a streamlined MLOps framework involving CI, CD and CT.
    <br />
    <a href="https://github.com/asheshd/MLOps-IISc-Movie_Recommender"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://asheshd-mlops-iisc-proj-ui-predict-movies-j2nd76.streamlitapp.com/">View Demo</a>
    ·
    <a href="https://github.com/asheshd/MLOps-IISc-Movie_Recommender">Report Bug</a>
    ·
    <a href="https://github.com/asheshd/MLOps-IISc-Movie_Recommender">Request Feature</a>
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#results">Usage</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>



<!-- ABOUT THE PROJECT -->
## About The Project
  The goal of the MLOps implementation for the recommendation system DNN is to be able to seamlessly verify any updates to the project, re-train it on cloud using web-hosted database, release a new model ready to be queried, and make it available immediately on a web app where user can access movie recommendations based on latest models.
  
The tools used in achieving this goal are presented in the figure below, along with the flow of control/data.


![IISc MLOps Project](https://user-images.githubusercontent.com/42042450/177289974-1e8c5308-74ca-432e-985d-670a19d0dd31.png)

<p align="right">(<a href="#top">back to top</a>)</p>

### The chain and the tools are as follow:
#### Database Access

The movielens database is already hosted on the web and is seamlessly accessible to the local workstation as well as to the cloud hosted repository.
    
#### Integration using GitHub and GitHub Actions and Training

GitHub is used for version control of the project's core ML training and model generation codes. Additionally, it is also maintaining the code to serve the updated model to the web application.
    
GitHub Actions is the main orchestrator in the flow. Whenever the repositories are updated, it runs the corresponding action scripts (.yaml). Whenever the main project is updated, the GitHub Actions workflow establishes an environment with python3 and installs all the requirements from the requirements.txt file. The requirements include libraries like tensorflow, keras, modelstore, boto3, and other common libraries. Tensorflow and keras are needed to execute the script for training the model from scratch on cloud. Boto3 and modelstore are required to generate the model in a format that AWS S3 supports for model hosting. Additionally, the keys required to make seamless access to AWS are defined in the yaml file while they are stored as secrets.
    
GitHub Actions also triggers the back-end project for the web application on every update. In order to setup the environment for calling the model from web application another set of requirements are installed which are same as the previous set of requirements. GitHub actions runs the script to call streamlit web application.
    
#### Model Deployment to AWS S3 bucket
The model is deployed to the Amazon AWS s3 bucket where it is launched to be consumed in any service. The modelstore library provides simple APIs to save and load the ML model from any authorised tool.
    
#### Model querying and serving on web
The web hosting application resides is called from GitHub Actions. The underlying script also loads the S3 model from AWS. Streamlit tool provides a fast and easy framework with many easy-to-use APIs that can be called from a python script. In this project, it is called from the GitHub project. It provides a simple and fast UI to query the underlying model and see the results immediately on the page.

### Web App

https://github.com/asheshd/MLOps-IISc-Proj-UI - A web UI project to serve model for AWS and make prediction for the top N movies recommendation.


### Built With

* [Python3](https://www.python.org/downloads/)
* [Tensorflow](https://www.tensorflow.org/install)
* [Keras](https://keras.io/)
* [Amazon AWS](https://aws.amazon.com/)
* [Github Action](https://github.com/features/actions)
* [Streamlit](https://streamlit.io/)
* [ModelStore](https://pypi.org/project/modelstore/)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- GETTING STARTED -->
## Getting Started

Follow the below steps to get started with the this Recommendation System MLOps project.

### Prerequisites

Here is a list of python packages required to sun this project.
* python
  ```sh
  numpy
  pandas
  boto3
  modelstore
  sklearn
  tensorflow==2.8.2
  keras==2.8.0
  ```

### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/asheshd/MLOps-IISc-Movie_Recommender.git
   ```
3. Install Python packages
   ```sh
   pip install -r requirements.txt
   ```
4. Run recommendation_system_mlops_project_with_deep_learning.py
   ```sh
   python recommendation_system_mlops_project_with_deep_learning.py
   ```
   
<p align="right">(<a href="#top">back to top</a>)</p>



<!-- USAGE EXAMPLES -->
## Results

The following screenshot shows the web application developed using Streamlit tool. The input to the tools are user-id (of a user with an existing account and movie rating data) and the number of new movies to be recommended. The interface updates in real time to present a list of movie recommendation for the user. The tool also allows to see the back-end queries in a terminal on the page.


![Web UI](https://user-images.githubusercontent.com/42042450/177300200-09b72246-f4b3-492b-a79d-38b245726d10.png)


_For more details, please refer to the [Web App](https://asheshd-mlops-iisc-proj-ui-predict-movies-j2nd76.streamlitapp.com/)_

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are **greatly appreciated**.

If you have a suggestion that would make this better, please fork the repo and create a pull request. You can also simply open an issue with the tag "enhancement".
Don't forget to give the project a star! Thanks again!

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

<p align="right">(<a href="#top">back to top</a>)</p>


<!-- LICENSE -->
## License

Distributed under the MIT License. See `LICENSE.txt` for more information.

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- CONTACT -->
## Contact

Ashesh Deep - asheshdeep@iisc.ac.in

Project Link: [https://github.com/asheshd/MLOps-IISc-Movie_Recommender](https://github.com/asheshd/MLOps-IISc-Movie_Recommender)

<p align="right">(<a href="#top">back to top</a>)</p>



<!-- ACKNOWLEDGMENTS -->
## Acknowledgments

* []()

<p align="right">(<a href="#top">back to top</a>)</p>
