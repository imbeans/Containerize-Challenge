FROM python:3

RUN mkdir -p /app01

WORKDIR /app01

COPY requirements.txt ./

RUN pip3 install -r requirements.txt

COPY . .

CMD [ "python3", "./index.py"]