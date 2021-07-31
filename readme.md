# Agile rails 6 shoppping cart depot

```
GEMS USED
gem 'bcrypt', '~> 3.1.7'
gem 'i18n-js'
```

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

```
GEMS USED
gem 'better_errors'
gem 'bulma-rails'
gem 'simple_form'
```

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
 before_action :configure_permitted_parameters, if: :devise_controller?

  protected

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:name])
    devise_parameter_sanitizer.permit(:sign_in, keys: [:name])
    devise_parameter_sanitizer.permit(:account_update, keys: [:name])
  end	
```

- styled devise forms with bulma
- used font awesome cdn
- user has gravatar image

<hr>

# Webcrunch - dribble clone

```
GEMS USED
group :development do
  gem 'better_errors', '~> 2.4'
  gem 'guard', '~> 2.14', '>= 2.14.1'
  gem 'guard-livereload', '~> 2.5', '>= 2.5.2', require: false
end

# gem 'carrierwave', '~> 1.2', '>= 1.2.1'
# gem "mini_magick"
gem 'impressionist'
gem "bulma-rails"
gem 'devise'
gem 'simple_form'
gem 'jquery-rails'
gem 'gravatar_image_tag'
gem 'acts_as_votable'

```

- devise added name
- devise forms with bulma
- Shots model
- comments Model
- shot id and user it to comments
- impressionist gem: rails g impressionist, rails db:migrate
- acts as votable: rails generate acts_as_votable:migration/rails db:migrate

```
adding js to specific pages
in the specific page
<h1 class='text-center'>I want my JS here only</h1>

<%= javascript_pack_tag 'hi' %>

create app/javascript/packs/hi.js
document.addEventListener("turbolinks:load", function() {
	console.log('in hi.js')
});


adding js file to everything
create the file all.js
document.addEventListener("turbolinks:load", function() {
	console.log('in all.js')
});

add to the packs/app.js file
import './all'
```

- added jquery rails to rails 6
- https://www.botreetechnologies.com/blog/introducing-jquery-in-rails-6-using-webpacker/
- added a verbose date helper
```
	def verbose_date(date)
		date.strftime('%B %d %Y')
	end
```

- added font awesome
- he used carrierwave cuz its rails 5, 
- im using active storage
- https://pragmaticstudio.com/tutorials/using-active-storage-in-rails

- gravatar image tag: 

```
<%= gravatar_image_tag(@shot.user.email, size: 20, alt: @shot.user.name, style: 'max-width: 40px') %>
```

- comments form in the shots
- acts as votable likes and unlike
- impressions to see how many viewers per page, a view count
- a hero banner based on whether the user is signed in or not
- I got the drop zone and preview to work, but the bulma css was messing it up, if im not using bulma, i dont have to trouble shoot it
- also the preview didnt work if i click on the box instead of drag and drop
- online suggests a plugin called: dropzone.js

<hr>

# Webcrunch - discussion forum

