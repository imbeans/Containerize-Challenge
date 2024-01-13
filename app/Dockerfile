# Using the official Python base image selected for long GA support - imbeans
FROM python:3.12-slim

RUN mkdir -p /app01

# Set the working directory in the container
WORKDIR /app01
# Expose port 8000 for Gunicorn
EXPOSE 8000

# Copy the requirements file into the container
COPY requirements.txt ./
# Install any needed packages specified in requirements.txt
RUN pip3 install -r requirements.txt

COPY . .
#allow hot-reloading via gunicorn
ARG options
ENV OPTIONS $options

#Start python, Load index, run gunicorn, bind port 8000 on all networks available to the container
#CMD [ "python3", "./index.py","gunicorn", "--bind", "0.0.0.0:8000", "server:app"] - testing out the below for hot-reloading
CMD ["sh", "-c", "exec gunicorn $OPTIONS python3 ./index.py --bind 0.0.0.0:8000 server:app"]
