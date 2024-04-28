#ERIC

Step 1 Install Flask using pip install Flask command

Step 2  Create a Flask App
create a file named app.py and define your Flask application

from flask import Flask

app = Flask(_name_)

@app.route('/')
def hello():
    return 'Hello, World!'

if _name_ == '_main_':
    app.run()

Step 3 Run The Flask App using python app.py command

step 4 create a test directory

step 5 create a test Python file test_app.py

import unittest
from app import app

class TestApp(unittest.TestCase):

    def setUp(self):
        self.app = app.test_client()

    def test_index(self):
        response = self.app.get('/')
        self.assertEqual(response.status_code, 200)
        self.assertEqual(response.data.decode('utf-8'), 'Hello, World!')

    def test_invalid_route(self):
        response = self.app.get('/invalid')
        self.assertEqual(response.status_code, 404)

if _name_ == '_main_':
    unittest.main()

step 6 Run the tests using python -m unittest discover tests

step 7 create a workflow file .github/workflow/ci-cd.yml

name: CI/CD Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: '3.x'

      - name: Install dependencies
        run: |
          pip install -r requirements.txt

      - name: Run tests
        run: |
          python -m unittest discover tests

      - name: Deploy to Heroku
        if: success()
        uses: akhileshns/heroku-deploy@v3.12.12
        with:
          heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
          heroku_app_name: ericwebapp
          heroku_email: omkar.rohokale5328@gmail.com

step 8 set up Heroku
Generate API key on Heroku and add it as a secret in your Github Repository with the name HEROKU_API_KEY

step 9 commit chabges into github repository

Adiitional notes
you need to include a procfile and any necessary dependancies in requirements.txt file



 


