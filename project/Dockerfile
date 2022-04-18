###########
# BUILDER #
###########

FROM python:3.9.6-alpine as builder

# work directory
WORKDIR /usr/src/app

# environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

RUN apk update \
	&& apk add tk \
	&& apk add postgresql-dev gcc python3-dev musl-dev

# lint
RUN pip3 install --upgrade pip
COPY . .

# install dependencies
COPY requirements.txt /tmp/requirements.txt
RUN pip3 wheel --no-cache-dir --no-deps --wheel-dir /usr/src/app/wheels -r /tmp/requirements.txt

#########
# FINAL #
#########

FROM python:3.9.6-alpine

# create directory for the app user
RUN mkdir -p /home/app

# create the app user
RUN addgroup -S app && adduser -S app -G app

# create the appropriate directories
ENV HOME=/home/app
ENV APP_HOME=/home/app/web
RUN mkdir $APP_HOME
RUN mkdir $APP_HOME/staticfiles
WORKDIR $APP_HOME

# install dependencies
RUN apk update \
	&& apk add tk \
	&& apk add libpq
	
COPY --from=builder /usr/src/app/wheels /wheels
COPY --from=builder /usr/src/app/requirements.txt .
RUN pip3 install --no-cache /wheels/*

# copy entrypoint-prod.sh
# COPY ./entrypoint.prod.sh $APP_HOME

# copy project
COPY . $APP_HOME

# chown all the files to the app user
RUN chown -R app:app $APP_HOME

# change to the app user
USER app

# run entrypoint.prod.sh
# ENTRYPOINT ["/home/app/web/entrypoint.prod.sh"]