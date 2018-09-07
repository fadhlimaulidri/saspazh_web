# Sinatra

Sinatra mysql

```
$cd ~/Desktop
$mkdir project-name
$cd project-name
$touch Gemfile
```
## Gemfile
```
source 'https://rubygems.org'

gem 'activerecord'
gem 'sinatra-activerecord'
gem 'sqlite3'
gem 'rake'
gem 'mysql2'
gem 'dotenv'
```

## Install the dependencies
```
$bundle install
```

## Create an app.rb file
```
require 'sinatra'
require 'sinatra/activerecord'
require 'dotenv/load'

set :database, {
	adapter: "mysql2", 
	host: ENV['MYSQL_HOST'],
	database: ENV['MYSQL_NAME'],
	username: ENV['MYSQL_USERNAME'],
	password: ENV['MYSQL_PASSWORD'],
    port: ENV['MYSQL_PORT'],
    pool: 50
}
```

## Rakefile
```
require 'sinatra/activerecord/rake'
require './app'
```

## Create a migration for creating a users table

$rake db:create_migration NAME=create_users_table

## Add code to the migration for creating columns
```
class CreateUsersTable < ActiveRecord::Migration[5.0]
  def change
    create_table :users do |t|
      t.string :fname
      t.string :lname
      t.string :email
      t.datetime :created_at
      t.datetime :updated_at
    end
  end
end
```
## Run the migration

$rake db:migrate

## Create a User model

#models.rb
```
class User < ActiveRecord::Base
end
```

## Load the User model into your app

#at the bottom of app.rb
```
require './models'
```

## Create a seeds file
```
$touch db/seeds.rb
```

## Write some seeds

#db/seeds.rb
```
users = [
  {fname: 'Jon', lname: 'Doe', email: 'e@example.com'},
  {fname: 'Jane', lname: 'Doe', email: 'e@example.com'}
]

users.each do |u|
  User.create(u)
end
```

## Run the seeds
```
$ rake db:seed
```

