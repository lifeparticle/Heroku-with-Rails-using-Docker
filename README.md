# Heroku-with-Rails-using-Docker

## Docker Setup
https://docs.docker.com/compose/rails/

1. Generate the Rails skeleton app using docker-compose run:

```
docker-compose run web rails new . --force --no-deps --database=postgresql
```

2. Build the image again (This, and changes to the Gemfile or the Dockerfile, should be the only times you’ll need to rebuild)

```
docker-compose build
```

3. Replace the contents of config/database.yml

```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```

4. Boot the app

```
docker-compose up
```

5. Create the database

```
docker exec -it pluto-corporation_web_1 /bin/bash
rake db:create
```

6. Push the repo to github

## Heroku Setup

1. Create a new app.
2. Under the app go to the resources tab and add Heroku Postgres.
3. Under the app go to the deploy tab and select GitHub as the Deployment method.
4. Choose between Automatic deploys or Manual deploy.
5. If you're using Rails Encrypted Credentials then under the app go to the settings tab and select add Config Vars and add RAILS_MASTER_KEY.
