# Performance Review API

Performance Review API is a backend side of performance review application; 
an application that allows employees to submit feedback toward each other's performance review.  

Written in ruby 2.72 with mysql for database

## Documentation

API documentation is provided inside `doc` folder, it has two files as follows:
  *  `index.html`: A static html file which contains API documentation, generated by [aglio](https://github.com/danielgtaylor/aglio)
  * `api/index.apib`: API documentation in API Blueprint format

Both of documentation is automatically generated by rspec tests with [rspec_api_documentation](https://github.com/SirusDoma/rspec_api_documentation).  
You can regenerate documentation by running `bundle exec rake docs:generate`. Node.js is required to generate html view with [aglio](https://github.com/danielgtaylor/aglio).

## Run application

There's several way to start the application, either with docker or manual setup.  
Note that you can use `db:create` and `db:migrate` if you do not wish to seed the table with fake data.

### Local

1. Copy `.env.sample` to `.env` and configure application setting
2. Install required gem with bundler, use `gem install bundler` if bundler is not installed then proceed with `bundle install`
3. Run `bundle exec rake db:setup` to run database migrations
4. Run `bundle exec -C config/puma.rb config.ru`
5. Press CTRL+C to stop the application

### Docker

1. Copy `.env.sample` to `.env` and configure application setting
2. Run `docker build -t performance-review-api .` to build application as docker image
3. Run `docker run --rm --env-file .env --entrypoint="" performance-review-api bundle exec rake db:setup` if database is not migrated yet
4. Run `docker run --rm --env-file .env -p 8000:8000 performance-review-api` to create new container and start it
5. Press CTRL+C to stop the application

Note: Development and test gems aren't included.

### Docker Compose

1. Copy `.env.sample` to `.env` and configure application setting
2. Run `docker-compose build` to build application and it's dependencies as docker image
3. Run `docker-compose up -d` to start application and it's dependencies in background
4. Run `docker-compose run --rm --entrypoint="" performance-review-api bundle exec rake db:setup` if database is not migrated yet.
   Make sure to give some time before execute the command to let mysql container start up
5. Run `docker-compose stop` in project directory to stop application and it's dependencies

Note: 
* Development and test gems aren't included
* Application may throw error if accessed before migration is executed.

## License

This is an open-sourced application licensed under the [MIT License](https://github.com/SirusDoma/Performance-Review-API/blob/master/LICENSE).
