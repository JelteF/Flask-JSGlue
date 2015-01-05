Flask-JSGlue
=============

Flask-JSGlue helps hook up your Flask application nicely with the front end.

Installation
-------------

Install the extension with one of the following commands::

    $ easy_install Flask-JSGlue

or alternatively if you have pip installed::

    $ pip install Flask-JSGlue 


Set Up
------

Glue codes are generated and managed through a ``JSGlue`` instance::

    from flask import Flask
    from flask_jsglue import JSGlue 

    app = Flask(__name__)
    jsglue = JSGlue(app)

You may also set up your ``JSGlue`` instance later at configuration time using **init_app()** method::

    jsglue = JSGlue()

    app = Flask(__name__)
    jsglue.init_app(app)

Invoking **url_for()** at the front-end side
--------------------------------------------------

**url_for()** is commonly used through the whole application to prevent being broken when routes are changed. Considering the fact that designing services in a RESTful manner is highly recommended nowadays, it's frustrating that you can't use **url_for()** at the front-end side. Especially when the routes are being frequently changed due to acitve development. Flask-JSGlue provides a client-side **url_for()**, which makes source codes dynamic, more charming.

In **<head>**::

    {{ JSGlue.include() }}

In your Javascript source code::

    Flask.url_for("static", {"filename": "jquery.min.js"})

    Flask.url_for("api.hello_world", {"param1": 1, "param2": "text"})

.. warning::

    Since it's being done at the front-end side, passing objects other than primitive types will raise an exception.

.. note::
    
    However, `the Flask documentation <http://flask.pocoo.org/docs/0.10/patterns/jquery/#where-is-my-site>`_ suggests that you just add a script tag to your webpage that has URLs. Perhaps you're wondering if Flask-JSGlue's approach is the right way of doing it, since it seems like the Flask documentation suggests the other simpler way. The answer is yes. Actually, it's the same way as what the documentation suggests. it's just a more sophisticated way of doing it than just adding a raw script tag.