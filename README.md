# Citizen Science Web Application

You can run the Python server with the command: 
```
**python main.py**
```
The server will listen for requests on: [http://localhost:8010]

The `cypress` directory contains tests to be run with the [Cypress](https://cypress.io) testing tool.

## **Requirements**

**RThis project requires Python 3**R
The bottle library is also required but is already included

## **The API Server**

The Python API server provides the following URLs serving JSON data:

* `/api/users` - GET returns a JSON array of user details
* `/api/users/<id>` - GET returns details of an individual user
* `/api/observations` - GET returns a JSON array of observation records
* `/api/observations` - POST adds a new observation record (required fields below)
* `/api/observations/<id>` - GET returns details of an individual observation
* `/api/reset` - GET request resets the database (for testing purposes)

A json observation object looks like:
{
    "id": 0,
    "participant": 6,
    "timestamp": "2020-04-05T01:11:52.659941",
    "temperature": 13,
    "weather": "sunny",
    "wind": "strong",
    "location": "Marsfield",
    "height": 24,
    "girth": 2.85,
    "leaf_size": "large",
    "leaf_shape": "divided",
    "bark_colour": "red",
    "bark_texture": "crinkles"
}

The fields in the form to submit to api are as follows:
* **participant** - participant id, should be a hidden field with the value 0 (since Bob is logged in)
* **temperature** - a numerical field
* **weather** - a select field with options for "fine", "raining", "sunny", "stormy"
* **wind** - a select field with options for "none", "light", "medium", "strong"
* **location** - a text input
* **height** - a floating point number
* **girth** - a floating point number
* **leaf_size** - a select field with options for "small", "medium", "large"
* **leaf_shape** - a select field with options for "rounded", "pointy", "divided"
* **bark_colour** - a select field with options for "grey", "red", "silver", "brown"
* **bark_texture** - a select field with options for "smooth", "peeling", "crinkles", "furry", "spotty"

## **The Web Application**

The main page of the application is generated by the Python code from the file `index.html` 
in the `views` folder.  You can edit this file to add anything you need to implement
your application. 

Static files are served from the `static` folder.  You will see sub-folders for CSS, Javascript
and images.   If you want to refer to one of these files in your HTML, use a URL 
like `/static/js/main.js` or `/static/css/style.css`.  The leading `/` is important.  You can
add any other sub-folders you might want under the `static` folder and it will be served
by the application.

There will be six views in the application, these are outlined here. Each page has a specific URL hash as shown here:
* **Main Page** (/): contains some summary information, list of recent observations, current top 10 leaderboard of users and a link to the form to add an observation.  The user and observation entries link to their individual views (user profile view and observation detail view).
* **Observation Form** (/#!/submit): a view containing the form to submit an observation. The user will fill out the form and submit it. If the form is incomplete, a list of errors will be shown above the form and the user will be able to fix them and resubmit.  If the submission is successful, the user is shown the User Profile View where the new observation will be included in the observation list.
* **User Profile View** (/#!/users/<id>): shows the brief details of the user (name, avatar) and a complete list of the observations they have made, most recent first, each observation links to the Observation Detail view
* **Observation Detail View** (/#!/observations/<id>): shows the full details of one observation including all fields
* **Observation List View** (/#!/observations): shows the complete list of observations, each observation includes at least the location and weather fields and links to the Observation Detail view
* **Leaderboard View** (/#!/users): lists the full list of users in order of the number of observations that they have made. Each entry links to the profile view for that user.

## **Java Scripts**

* **form.js**: This JS file contains functions used by the form to submit an observation
* **main.js**: The main redraw function, window events and listeners
* **model.js**: All functions to interact with the API for observations and users
* **util.js**: Contains split_hash utility function to split hash and id
* **views.js**: Each of the views used by html templates to generate html dynamically

.
