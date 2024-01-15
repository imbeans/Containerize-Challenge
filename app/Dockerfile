# Using the official Python base image selected for long GA support - imbeans
FROM python:3.12-slim

# Set the working directory in the container
WORKDIR /app

# set env variables
ENV FLASK_ENV=development
ENV DEBUG=true

# Expose port 8000 for Gunicorn
EXPOSE 8000


#allow hot-reloading via gunicorn
ARG options
ENV OPTIONS $options

# At runtime install the modules from requirements.txt && then start the server.py via gunicorn and specify the --reload option for hot reload
CMD /bin/bash -c "pip3 install --no-cache-dir -r /app/src/requirements.txt && gunicorn -k gevent --bind 0.0.0.0:8000 --reload $OPTIONS src.server:app"







