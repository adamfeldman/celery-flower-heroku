# Celery Flower monitoring for Heroku

[Flower](https://github.com/mher/flower/) is a handy tool for monitoring [Celery](http://www.celeryproject.org/) processes. As it's build on top of Tornado web server it needs it's own outside facing port and can't be run as part of your regular Heroku app which only provides one ```web``` process type. Luckily Flower is really easy to install as another app and can be run free of charge on Heroku.

This project template/guide helps you to bootstrap the process and creates a simple app for running Flower.

Clone the repo:

    git clone https://github.com/jorilallo/celery-flower-heroku.git

Create an Heroku app:

    heroku create APP_NAME

Configure the app by providing your broker url (RabbitMQ, Redis, what have you) and a password for logging into Flower:

    heroku config:set BROKER_URL=redis://...
    heroku config:set FLOWER_BASIC_AUTH="username:password"

Push to heroku:

    git push heroku master

Now visit the app. It will ask for a username and a password which you defined above.

Although Flower's persistence is enabled, it depends on writing to the local filesystem, [which is ephemeral on Heroku](http://stackoverflow.com/questions/12416738/how-to-use-herokus-ephemeral-filesystem). Therefore the persisted data will be lost when your Heroku Dyno restarts, for example after deploying config or code changes. However Flower persistence is [mostly a convenience feature](http://flower.readthedocs.io/en/latest/config.html#persistent).
