FROM sphinxdoc/sphinx
LABEL maintainer="The Rockstor Project <https://rockstor.com>"
LABEL org.opencontainers.image.authors="The Rockstor Project <https://rockstor.com>"

WORKDIR /docs

# Install git for sphinxext-rediraffe builders
RUN apt-get update \
 && apt-get install --no-install-recommends -y \
      git \
 && apt-get autoremove \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

ADD requirements.txt /docs
RUN pip3 install -r requirements.txt
