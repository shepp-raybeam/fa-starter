# Example Angular-on-Flask Starter

This repository contains a quickstart angular + flask application that can be
deployed to AppEngine on the Google Cloud Platform.

You will need to install python3, node, ng cli, and the gcloud sdk to use it.
Additionally you will need a [Google Cloud](https://console.cloud.google.com/freetrial) account.

## Server setup

I recommend you use a [venv](https://docs.python.org/3/library/venv.html) while developing with this repo.
One way to do this is in the command listing below.

```
virtualenv venv
source venv/bin/activate
cd server
python -m pip install -r requirements.txt
```

Now you can run the server locally:

```
flask run
```

configure flask and your backend variables in .flaskenv (see example.flaskenv) and app/config.py

## Client setup

In another terminal, build and serve the client.

```
cd client
npm install
ng serve -c dev
```

If http://localhost:4200 serves you 'example works!' and http://localhost:4200/api/ serves you 'hello', everything is set up right.
If you get error occured while trying to proxy, probably you don't have flask running - do `flask run` in another terminal from the server dir

Now we are going to make it so you can deploy to gcp, by creating a production client build with

```
cd client
ng build --prod
```

files in server/dist/client should be created

## GCP setup

Once you have the [Cloud SDK](https://cloud.google.com/sdk/docs/install)
installed and your GCP account created, run `gcloud init` to create a default
configuration. In this process you will log in to your GCP account and create
a new GCP project.

ensure all build steps are done:

```
cd client
ng build --prod
cd ../server
pip install -r requirements.txt
```

deploy to cloud

```
cd server
gcloud app deploy
```

now you should be able to access the app hosted in gcp via the 2 endpoints `/` and `/api/`
