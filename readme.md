# Agile rails 6 shoppping cart depot

- ajax the shopping cart
- action cable to update prices without refreshing the page (had to make it in {formatting} to work in ruby 3, I was getting an error)
- added atom feed (like rss) for the orders
- added react for pay selector
- installed mailcatcher
- to see emails http://127.0.0.1:1080
- set up an order and shipped email
- connecting to a slow payment processor with active job
- added users with sessions
- used enums	
- validates images uploads
- validations
- added admins
- internationalization
- used gem 'i18n-js' for react
- https://github.com/svenfuchs/rails-i18n/tree/master/rails/locale
- received emails with rich text/ action text

```
How Are Background Jobs Run in Development or Production?
When running the application locally, the background jobs are executed and emails are sent by Rails. By default, Rails uses an in-memory queue to manage the jobs. This is fine for development, but it could be a problem in production. If your app were to crash before all background jobs were processed or before emails were sent, those jobs would be lost and unrecoverable.
In production, you’d need to use a different back end, as detailed in the Active Job ab
Rails Guide. Sidekiq is a popular open-source back end that works great. Setting
it up is a bit tricky, since you must have access to a Redis database to store the
c
waiting jobs. If you are using Postgres for your Active Records, Queue Classic is
another option for a back end that doesn’t require Redis—it uses your existing Postgres
d
a. http://guides.rubyonrails.org/active_job_basics.html#job-execution
b. http://sidekiq.org/
c. https://redis.io/
d. https://github.com/QueueClassic/queue_classic/tree/3-1-stable
database.

```

<hr>

# Webcrunch - demo blog

- posts
- with nested comments dependent destroy
- bulma css

<hr>

# Webcrunch - twitter

```
GEMS USED
gem 'bulma-rails'
gem 'simple_form'
gem 'gravatar_image_tag'
gem 'devise'
gem 'better_errors'
```

- tweeets model
- users with devise
- added fields to devise, name username and uniqueness column
- rails g migration add_fields_to_users name username:uniq  
- tweets build from current user
- devise permitted

```
    devise_parameter_sanitizer.permit(:sign_up, keys: [:name, :username])
    devise_parameter_sanitizer.permit(:account_update, keys: [:name, :username])
```

- styled devise forms with bulma
- used font awesome cdn
- user has gravatar image

<hr>