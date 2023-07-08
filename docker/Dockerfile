FROM squidfunk/mkdocs-material:9.0.6

RUN apk add --no-cache bash

COPY .github/requirements.txt /requirements.txt

RUN pip install -r /requirements.txt

