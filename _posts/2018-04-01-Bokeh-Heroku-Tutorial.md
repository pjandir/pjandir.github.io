---
 layout: post
 title: Deploying a Flask and Bokeh app to Heroku
---


I have been wanting to build a simple web app with some interactivety for a while now. I used a few different tutorials/demos to build this kind of app. Specifically, I used Bokeh, an interactive Javascript based visualization library, and Flask to build a web app and then deploy it to Heroku, a cloud platform for web apps (and more). 

The Data Incubator (TDI) has a recipe for this process on their [blog](https://blog.thedataincubator.com/2015/09/painlessly-deploying-data-apps-with-bokeh-flask-and-heroku/), but there is some missing steps as well as a significant (but fixable) error. To help fill the gaps, there is a great step-by-step tutorial by the Stanford Computational Journalism Lab (SCJL) on their GitHub [page](https://github.com/datademofun/heroku-basic-flask). This tutorial can be followed to deploy a simple Flask app on Heroku. In fact, aside from using Bokeh in particular, there is very little difference between the SCJL tutorial and this one. So, I will try not repeat that information, since its already well done. Note also these tutorials have links to other related tutorials as well, for even more information. 

## Step 1: Creating Heroku account

It should go without saying that we will need to first create an account on [Heroku](https://www.heroku.com/home) before we can deploy anything on their platform. While paid options exist, we can, without a credit card, deploy 
for free as well! This step is unaltered from the SCJL tutorial.

## Step 2: Building Flask app

We can create a simple Flask app like the one shown in the SCJL tutorial. But now we want to use the outline given in the TDI tutorial and setup Bokeh. 

### The python script

A full working python script is shown below. Since this web app is just a python script, we can also run it to test it like any other python script: by calling it from the command line. 


```python
#Load the packages
import pandas as pd
from flask import Flask, render_template
from bokeh.embed import components 
from bokeh.models import HoverTool
from bokeh.charts import Scatter

#Connect the app
app = Flask(__name__)

#Helper function
def get_plot(df):
    #Make plot and customize
    p = Scatter(df, x='sepal_length', y='sepal_width', xlabel='Sepal Length [cm]', 
                ylabel='Sepal Width [cm]', title='Sepal width vs. length')
    p.title.text_font_size = '16pt'
    p.add_tools(HoverTool()) #Need to configure tooltips for a good HoverTool

    #Return the plot
    return(p)

@app.route('/')
def homepage():

    #Get the data, from somewhere
    df = pd.read_csv('https://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data', 
                     names=['sepal_length', 'sepal_width', 'petal_length', 'petal_width', 'class'])

    #Setup plot    
    p = get_plot(df)
    script, div = components(p)

    #Render the page
    return render_template('home.html', script=script, div=div)    

if __name__ == '__main__':
    app.run(debug=True) #Set to false when deploying
```

Let's go through it. The app will run the homepage() function which here loads into a *pandas* dataframe the (classic) iris dataset from the UCI Machine Learning Repository. This dataframe is then passed into the get_plot() function which returns a Bokeh plot. This is where our interactive plot is created and customized however we wish. In this case we just make a scatter plot of the sepal width versus the sepal length (ignoring the iris type or class). Bokeh is great because we can extract the guts of the plot (from the Bokeh's components() method) and throw it into an HTML document to render. This is what Flask's render_template() method is doing for us. It calls the home.html (located in the templates subfolder) with the provided arguments. 

### The html file

What does this home.html file look like?


```python
<html>
  <head>
    <!-- <link rel="stylesheet" href='{ url_for('static', filename='style.css')}' type="text/css" /> -->
    <link rel="stylesheet" href="//cdn.pydata.org/bokeh/release/bokeh-0.12.4.min.css" type="text/css" />
    <script type="text/javascript" src="//cdn.pydata.org/bokeh/release/bokeh-0.12.4.min.js"></script>
    {{ script | safe }}
  </head>
  <body>
    <div class=page>
      <h1>The iris dataset and Bokeh</h1>
      {{ div | safe }}
    </div>
  </body>
</html>
```

This HTML file is very similar to the one from the TDI tutorial, but a few notes must be made. First, the script and stylesheet used to load in the Bokeh JavaScript library must use the exact same version as your local machine. Second, the reference should not include the 'http' portion, as modern browers have issues with that. Credit to this goes to [davidism](https://stackoverflow.com/a/33452391/6477651) from Stack Overflow. Third, we can include our own stylesheet using the commented out link above the stylesheet from Bokeh. Remember, at the end of the day this file is just HTML, so we can customize this however we want. With these files, we should now be able to run the app and serve it on your localhost! 


```python
$ python app.y
```

## Step 3: Setting up app for Heroku

Now that we have a working app, we can worry about deploying it to Heroku. The rest of this tutorial follows the SCJL tutorial nearly exactly. Please refer to it for more details. We will need three files: Procfile, runtime.txt, and requirements.txt for Heroku to set everything up correctly. 

### The requirements.txt file

The requirements.txt file is the usual file specifying which packages are needed. In our case, we need to list the three packages we used to build our app: Flask, pandas, and Bokeh. In addition we need to specify (and install if you do not have it) gunicorn. Heroku needs this last library so including this should ensure everyone plays nice. So our requirements.txt will look something like this.


```python
Flask==0.12
pandas==0.19.2
bokeh==0.12.4
gunicorn==19.7.1
```

Note, that I also specified the package version. Its not required (I don't think..), but I think its good to make sure the same conditions of your local machine are replicated on Heroku. This again helps ensure everyone plays nicely with each other. 

### The runtime.txt and Procfiles

The runtime.txt and Procfiles are the same as the one found in the SCJL tutorial. Note of course your specific python version should be used in the runtime.txt file. 

### Testing the app in Heroku

We can test the app, again, by issuing the local subcommand.


```python
$ heroku local web
```

This makes sure the app still works (on your localhost) in the Heroku framework. We are almost ready to deploy!

## Step 4: Deploying to Heroku

Now, we can initialize a git repo (not GitHub, just git!) in our working directory. Add all relevant files and commit. We can issue the create subcommand to, well, create the app. 


```python
$ heroku create
```

This sets up a blank app (with a rather random name) that you can now access. Now you just want to push your repo to Heroku like usual.


```python
$ git push heroku master
```

Now the entire app will be setup on Heroku following the rules setup in the three files from Step 3. Since everything is going to be installed from scratch, it can take upwards of a few minutes. After it finishes, we are done! You should now be able to check your app in your browser and the interactive Bokeh plot. Woohoo! You can now make any needed changes to your app. Push your changes as you would any other git repo to update the app on Heroku. 

### Changing the app name

We may want to change the name of our app to something more sensible. You can do this easily on Heroku's web dashboard. Login to your Heroku account and go to your dashboard. Click on your app and then click on the Settings tab on the ensuing screen. Here we can edit the name of the app. Change it to whatever (unique) name you want. You will then get a warning about git remotes from Heroku. To change your git remotes, simply issue these commands at the command line. 


```python
$ git remote rm heroku
$ heroku git:remote -a my-awesome-new-app-name
```

And that's it. You should have an awesome web app running a Bokeh plot on Heroku. A full working example with a simple customized stylesheet using all this code can be found on my GitHub [here](https://github.com/pjandir/projects/tree/master/Bokeh-Heroku-Tutorial). 

Happy developing! 

