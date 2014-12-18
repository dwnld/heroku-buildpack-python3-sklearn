Heroku buildpack: Python 3 with scikit-learn
============================================

This is a [Heroku buildpack](http://devcenter.heroku.com/articles/buildpacks) for Python 3 apps with scikit-learn.

Usage
-----

We use [buildpack-multi](https://github.com/heroku/heroku-buildpack-multi) and 
[buildpack-apt](http://github.com/ddollar/heroku-buildpack-apt) to install the apt-packages 
`python3-numpy` and `python3-scipy`.

Set your app's buildpack to use `buildpack-multi`:

    $ heroku config:set BUILDPACK_URL=https://github.com/heroku/heroku-buildpack-multi.git

Let `buildpack-multi` knows that you will need to use at least the two following buildpacks:

    $ echo -e "https://github.com/ddollar/heroku-buildpack-apt\nhttps://github.com/dwnld/heroku-buildpack-python3-sklearn" > .buildpacks

Create an [Aptfile](http://github.com/ddollar/heroku-buildpack-apt) in your project's root directory and add the following apt-packages:

    python3-setuptools
    python3-pip
    python3-numpy
    python3-scipy
    libatlas-dev
    libatlas3gf-base

Append scikit-learn to your `requirements.txt` if you haven't already done so:

    echo "scikit-learn" >> requirements.txt

Add the new files to your repo:
    
    git add .buildpacks Aptfile requirements.txt

That's it! You should now be able to use scikit-learn on heroku after deployment.

Python 2.7
-----------

If you are using Python 2.7, I recommend that you use https://github.com/thenovices/heroku-buildpack-scipy
