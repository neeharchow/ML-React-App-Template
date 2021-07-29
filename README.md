# ML-React-App
It's a template on which we can build a React app and call endpoints to make predictions.

### Usage
The complete guide to use this repository: https://towardsdatascience.com/create-a-complete-machine-learning-web-application-using-react-and-flask-859340bddb33

https://towardsdatascience.com/create-a-complete-machine-learning-web-application-using-react-and-flask-859340bddb33

Towards Data Science


Upgrade

Follow
564K Followers
·
Editors' Picks
Features
Deep Dives
Grow
Contribute
About






You have 1 free member-only story left this month. Upgrade for unlimited access.

Create a complete Machine learning web application using React and Flask
Karan Bhanot
Karan Bhanot

Apr 16, 2019·6 min read





Photo by Alvaro Reyes on Unsplash
I have always wanted to develop a complete Machine learning application where I would have a UI to feed in some inputs and the Machine learning model to predict on those values. Last week, I did just that. In the process, I created an easy to use template in React and Flask, that anyone can modify to create their own application in a matter of minutes.
Highlights of the project:
The front-end is developed in React and would include a single page with a form to submit the input values
The back-end is developed in Flask which exposes prediction endpoints to predict using a trained classifier and send the result back to the front-end for easy consumption
The GitHub repo is below. Fork the project and create your own application today!
kb22/ML-React-App-Template
It's a template to build a React app and interact with REST endpoints to make predictions. - kb22/ML-React-App-Template
github.com

Template
React
React is a JavaScript library created by Facebook to help make working with User interfaces simple and easy to develop and use. It’s one of the leading languages for front-end development. You can read about it here. The best resource to learn about React is its documentation itself which is very comprehensive and easy to grasp.
Flask and Flask-RESTPlus
Flask and Flask-RESTPlus allow us to define a service in Python which will have endpoints which we can call from the UI. You can learn more about developing a Flask app from my article below.
Working with APIs using Flask, Flask RESTPlus and Swagger UI
An introduction to Flask and Flask-RESTPlus
towardsdatascience.com

Description
I used create-react-app to create a basic React app to begin with. Next, I loaded bootstrap which allows us to create responsive websites for each screen size. I updated the App.js file to add a form with dropdowns and Predict and Reset Prediction buttons. I added each form property to state and on pressing the Predict button, I send the data to the Flask backend. I also updated the App.css file to add style to the page.

Template view
The Flask app has a POST endpoint /prediction. It accepts the input values as a json, converts it into an array and returns to the UI. In actual application, we’ll use the same data to make prediction using the classifier stored in classifier.joblib and return the prediction.

Prediction displayed on UI
Reset Prediction will remove the prediction from the UI.
Starting the template
Clone the repo to your computer and go inside it and open two terminals here.
Preparing the UI
In the first terminal, go inside the ui folder using cd ui. Make sure you are using the node version 10.4.1. Once inside the folder, run the command yarn install to install all dependencies.
To run the UI on server, we will use serve. We will begin by installing the serve globally, post which, we’ll build our application and then finally run the UI using serve on port 3000.
npm install -g serve
npm run build
serve -s build -l 3000
You can now go to localhost:3000 to see that the UI is up and running. But it won’t interact with the Flask service which is still not up. So, let’s do that.

UI
Preparing the service
On the second terminal, move inside the service folder using cd service. We begin by creating a virtual environment using virtualenv and Python 3. You can read about virtualenv here. We will then install all the required dependencies using pip after activating the environment. Finally, we’ll run the Flask app.
virtualenv -p Python3 .
source bin/activate
pip install -r requirements.txt
FLASK_APP=app.py flask run
This will start up the service on 127.0.0.1:5000.

Service
Voila! The complete application will now be working properly. Yaay!!
Using the template for own use case
To understand the process of using the template for any model, I’ll use the iris dataset and create a model for the same. This example is also available in the example folder in the project.
Create the model
I trained a DecisionTreeClassifier on the iris dataset which requires 4 features — Sepal Length, Sepal Width, Petal Length and Petal Width. Then, I saved the model to classifier.joblib using joblib.dump(). The classifier can now be used to predict on new data.
Update the service
Next, I opened the file app.py in a text editor (Sublime Text is one). I uncommented the line classifier = joblib.load(‘classifier.joblib’) so that the variable classifier now holds the trained model.
In the post method, I made the following updates:

Firstly, I used classifier.predict() to get the prediction. Next, I created a map for the classes such that 0 means Iris Setosa, 1 means Iris Versicolour and 2 means Iris Virginica. I finally returned the prediction in the result key.
Update: As pointed out by 
Martins Untals
, I forgot to mention that we also need to update the model so that it works correctly and has the updated model in Swagger UI.

As can be seen in the gist, I’ve updated the field names, their type to Float, description and help text. The same will now be reflected in Swagger too.

Updated model in Swagger UI
Update the UI
The form is made up of columns inside rows. Thus, as I have 4 features, I added 2 columns in 2 rows. The first row will have dropdowns for Sepal Length and Sepal Width. The second row will have dropdowns for Petal Length and Petal Width.
I began by creating a list of options for each of these dropdowns.

Next, I defined two rows with two columns each. Each dropdown selection will look like the code below:
For each dropdown, we’ll have to update the text inside <Form.Label></Form.Label>. We’ll name each selection group as well. Let’s say the name be petalLength so we set the value as {formData.petalLength} and name as “petalLength”. The options are added using the names we defined above inside <Form.Control></Form.Control> as we can see {petalLengths} above. Two such groups inside a <Form.Row></Form.Row> will make our UI.
The state must also be updated with the same names inside formData with the default values as the smallest value of the respective dropdowns. The constructor will look like below. As you can see, the state has been updated to have formData with new keys.
Add a new background image and title
Inside app.css, change the link of the background image to your own. I added an image of flowers from Unsplash. I also updated the title to Iris Plant Classifier and the page title too inside index.html file in the public folder.
Result
The application is now ready to use the model. Restart both services after building the UI using npm run build. The application looks like below:

Main Page
With some feature values, on pressing the Predict button, the model classifies it as Iris Setosa.

With new feature values, the model predicts the plant to be Iris Versicolour.

Conclusion
As you can see, in this article, I discussed a ML React App template that will make creating complete ML applications simple and quick.
Try the application for your own use case and share your feedback. I’d love to hear from you.
Sign up for The Variable
By Towards Data Science
Every Thursday, the Variable delivers the very best of Towards Data Science: from hands-on tutorials and cutting-edge research to original features you don't want to miss. Take a look.


Get this newsletter
Emails will be sent to narenchaudhry@gmail.com.Not you?

2.7K


22




Python
React
Technology
Development
Machine Learning
More from Towards Data Science

Follow
Your home for data science. A Medium publication sharing concepts, ideas and codes.

Read more from Towards Data Science
About

Write

Help

Legal

You can now make lists to organize and share stories.

Got it

