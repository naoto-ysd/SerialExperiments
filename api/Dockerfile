FROM ruby:2.7.1-alpine

# Define variable in Dockerfile
ARG WORKDIR
ARG RUNTIME_PACKAGES="nodejs tzdata postgresql-dev postgresql git"
ARG DEV_PACKAGES="build-base curl-dev"

# ENV is for defining environment variable.(ENV can refer in Dockerfile and container)
ENV HOME=/${WORKDIR} \
    LANG=C.UTF-8 \
    TZ=Asia/Tokyo

WORKDIR ${HOME}

# Copy files from host to container
COPY Gemfile* ./

# apk is commane for Alpine linux
RUN apk update && \
    apk upgrade && \
    apk add --no-cache ${RUNTIME_PACKAGES} && \
    apk add --virtual build-dependencies --no-cache ${DEV_PACKAGES} && \
    bundle install -j4 && \
    apk del build-dependencies

COPY .. ./

CMD ["rails", "server", "-b", "0.0.0.0"]
