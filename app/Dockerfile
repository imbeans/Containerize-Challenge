# Using the official Python base image selected for long GA support - imbeans
FROM python:3.12-slim

# Install system dependencies for gevent
#RUN apt-get update && \
#    apt-get install -y libev-dev gcc

# Create a non-root user
#RUN useradd -m beans

# Create Directory for the app
RUN mkdir -p /app01

# Grant ownership to the non-root user
#RUN chown -R beans:beans /app01

# Switch to the non-root user
#USER beans

# Set the working directory in the container
WORKDIR /app01

# Expose port 8000 for Gunicorn
EXPOSE 8000

# Copy the requirements file into the container
COPY /src/requirements.txt ./
# Install any needed packages specified in requirements.txt
RUN pip3 install -r requirements.txt

COPY . .
#allow hot-reloading via gunicorn
ARG options
ENV OPTIONS $options


#Start python, Load index, run gunicorn, bind port 8000 on all networks available to the container
#CMD [ "python3", "./index.py","gunicorn", "--bind", "0.0.0.0:8000", "index:app"] 
CMD ["gunicorn", "-k", "gevent", "--bind", "0.0.0.0:8000", "src.server:app"]




