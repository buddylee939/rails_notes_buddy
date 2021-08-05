# Book Agile rails 6 shoppping cart depot

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

# Book - take my money

- used monetize for the price column, with money_rails gem

```
rails generate model ticket \
  user:references performance:references \
  status:integer access:integer price:monetize

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
in application controller
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

```
GEMS USED
gem 'bulma-rails'
gem 'simple_form'
gem 'devise'
gem 'gravatar_image_tag'
gem 'jquery-rails'
gem 'rolify'
gem 'cancancan'
gem 'friendly_id'
gem 'redcarpet'
gem 'coderay'

```

- yarn install jquery
- https://www.botreetechnologies.com/blog/introducing-jquery-in-rails-6-using-webpacker/
- devise added username
- custom bulma functions
- added roles with rolify and cancancan
- searched discussions where channel id equals the current show

```
  def show
    @discussions = Discussion.where('channel_id = ?', @channel.id)
    @channels = Channel.all
  end
```

- discussions build from current user

```
  def new
    @discussion = current_user.discussions.build
  end
  def create
    @discussion = current_user.discussions.build(discussion_params)

```

- the replies in the discussions are done via js without refresh ajax

```
  def create
    @reply = @discussion.replies.create(params[:reply].permit(:reply, :discussion_id))
    @reply.user_id = current_user.id

    respond_to do |format|
      if @reply.save
        format.html { redirect_to discussion_path(@discussion) }
        format.js # renders create.js.erb
      else
        format.html { redirect_to discussion_path(@discussion), notice: "Reply did not save. Please try again."}
        format.js
      end
    end
  end
$("<%= escape_javascript(render(@reply)) %>").appendTo('#discussion-replies');
// clears out the textarea
$("#reply_reply").val(''); 

```

- used redcarpet and coderay to add markdown
- used different helpers for the roles

```
in application helper
  def has_role?(role)
    current_user && current_user.has_role?(role)
  end

in discussions helper
  def discussion_author(discussion)
    user_signed_in? && current_user.id == discussion.user_id
  end

  def reply_author(reply)
    user_signed_in? && current_user.id == reply.user_id
  end
```

- cancancan ability.rb

```
class Ability
  include CanCan::Ability

  def initialize(user)
      user ||= User.new # guest user (not logged in)
      if user.has_role? :admin
        can :manage, :all
      else
        can :read, :all
      end

  end
end
```

- friendly id, changing id if file changes

```
in channel.rb
  def should_generate_new_friendly_id?
    channel_changed?
  end
```

- rolify: role.rb

```
class Role < ApplicationRecord
  has_and_belongs_to_many :users, :join_table => :users_roles


  belongs_to :resource,
             :polymorphic => true,
             :optional => true


  validates :resource_type,
            :inclusion => { :in => Rolify.resource_types },
            :allow_nil => true

  scopify
end
```

- users has many through

```
user.rb
  has_many :discussions, dependent: :destroy
  has_many :channels, through: :discussions

```

- used gravatar images

```
<%= gravatar_image_tag(reply.user.email, class: 'border-radius-50', size: 48, alt: reply.user.username) %>

```

- devise bulma styling
- channel select dropdown with simple form, used a collection

```
  <div class="field">
    <label class="label">Channel</label>
    <div class="control has-icons-left">
      <span class="select">
        <%= f.input_field :channel_id, collection:@channels.map { |c| [c.channel, c.id] }, prompt: "Select channel" %>
      </span>
      <span class="icon is-small is-left">
        <i class="fa fa-tag"></i>
      </span>
    </div>
  </div>
```

- used a time ago in words

```
<p><em><small>Posted <%= time_ago_in_words(discussion.created_at) %> ago in
  <% if discussion.channel %>
    <%= link_to discussion.channel.channel, discussion.channel %>
  <% end %>
  by <%= discussion.user.username %>
  </small>
```

# Webcrunch - flanger

```
GEMS USED
gem 'bulma-rails', '~> 0.6.1'
gem 'simple_form', '~> 5.0'
gem 'devise', '~> 4.7'
gem 'gravatar_image_tag', '~> 1.2'
# gem 'carrierwave'
# gem 'mini_magick'

```

- added precision to price

```
t.decimal :price, precision: 5, scale: 2, default: 0
```

- generating without stylesheet or javascript

```
$ rails g scaffold Instrument brand:string model:string description:text condition:string finish:string title:string price:decimal --no-stylesheets --no-javascripts

rails g scaffold Cart --no-stylesheets --no-javascripts
```

- added instrument images
- bulma functions
- added a shopping cart
- no payment option though
- used active storage
- https://pragmaticstudio.com/tutorials/using-active-storage-in-rails

- shopping cart icon with a count
- application helpers
- instrument helper to check if the user who created it is the same as the current user

```
  def instrument_author(instrument)
    user_signed_in? && current_user.id == instrument.user_id
  end

```

- used javascript to fade out the notifications

```
document.addEventListener("turbolinks:load", function() {

  var notification = document.querySelector('.global-notification');

  if(notification) {
    window.setTimeout(function() {
      notification.style.display = "none";
    }, 4000);
  }

});
```

- added an image preview when uploading
- created a models/concern/current_cart.rb

```
module CurrentCart

  private

  def set_cart
    @cart = Cart.find(session[:cart_id])
  rescue ActiveRecord::RecordNotFound
    @cart = Cart.create
    session[:cart_id] = @cart.id
  end
end
```

- belongs to user optional

```
  belongs_to :user, optional: true
```

- used variables in the models

```
  BRAND = %w{ Fender Gibson Epiphone ESP Martin Dean Taylor Jackson PRS  Ibanez Charvel Washburn }
  FINISH = %w{ Black White Navy Blue Red Clear Satin Yellow Seafoam }
  CONDITION = %w{ New Excellent Mint Used Fair Poor }

```

- simple form collections

```
        <div class="columns">
          <div class="field column is-4">
            <div class="control">
              <label class="label">Brand</label>
              <div class="control has-icons-left">
                <span class="select">
                  <%= f.input_field :brand, collection: Instrument::BRAND, prompt: "Select brand" %>
                </span>
                <span class="icon is-small is-left">
                  <i class="fa fa-tag"></i>
                </span>
              </div>
            </div>
           </div>

          <div class="field column is-4">
            <div class="control">
              <label class="label">Finish</label>
              <div class="control has-icons-left">
                <span class="select">
                  <%= f.input_field :finish, collection: Instrument::FINISH, prompt: "Select finish" %>
                </span>
                <span class="icon is-small is-left">
                  <i class="fa fa-paint-brush"></i>
                </span>
              </div>
            </div>
           </div>

          <div class="field column is-4">
            <div class="control">
              <label class="label">Condition</label>
              <div class="control has-icons-left">
                <span class="select">
                  <%= f.input_field :condition, collection: Instrument::CONDITION, prompt: "Select condition" %>
                </span>
                <span class="icon is-small is-left">
                  <i class="fa fa-paint-brush"></i>
                </span>
              </div>
            </div>
           </div>
         </div>


```

- bulma devise forms
- used font awesomes

<hr>

# Webcrunch - job board with stripe

```
GEMS USED
gem 'devise'
gem 'bulma-rails'
gem 'simple_form'
gem 'gravatar_image_tag', github: 'mdeering/gravatar_image_tag'
gem 'sidekiq'
# gem 'carrierwave', '~> 1.0'
# gem 'mini_magick', '~> 4.8'
gem 'stripe'
# gem 'trix', '~> 0.11.1'
# gem "figaro"
```

- added the app name in the config/application.rb file

```
module WebcrunchJobBoard
  class Application < Rails::Application
    # Initialize configuration defaults for originally generated Rails version.
    config.load_defaults 6.1
    config.application_name = 'Job Board'

```

- used the editor to edit credentials and rails console to see that it worked

```
EDITOR="subl -w" rails credentials:edit

rails c
Rails.application.credentials.config[:stripe_publishable_key]
```

<hr>

# ABC Course - book review - in master-all-tutorials

```
GEMS USED
gem 'bootstrap-sass', '~> 3.3', '>= 3.3.7'
gem 'simple_form', '~> 3.5'
gem 'devise', '~> 4.3'

```

- books build by user

```
    @book = current_user.books.build(book_params)
```

- categories mapped, 

```
  def edit
    @categories = Category.all.map{ |c| [c.name, c.id] }    
  end

  <% if current_page?(new_book_path) %>
    <%= select_tag(:category_id, options_for_select(@categories), :prompt => "Select a category") %>
  <% else %>
    <%= f.select :category_id, @categories %>
  <% end %>

```

- select tag with options

```
    <%= select_tag "credit_card", options_for_select([ "VISA", "MasterCard" ], "VISA") %>  

```

- bootstrap navbar

<hr>

# ABC Course - listings - in master-all-tutorials

- validation

```
  validates :title, presence: true
  validates :description, presence: true

```

- select tag right in the form

```
  <div class="form-group">
    <%= f.label :category %>
    <%= f.collection_select :category_id, Category.all, :id, :name, { include_blank: "Please select..."}, { class: 'form-control' } %>
  </div>

```

- # ABC Course - photogram - in master-all-tutorials

```
GEMS USED - i didn't, only simple and devise
gem 'haml', '~> 5.0', '>= 5.0.1'
gem 'paperclip', '~> 5.1'
gem 'simple_form', '~> 3.5'
gem 'bootstrap-sass', '~> 3.3', '>= 3.3.7'
gem 'devise', '~> 4.3'
gem 'html2haml', '~> 2.2'
```

- i did active storage
- https://pragmaticstudio.com/tutorials/using-active-storage-in-rails
- added image processing gem and imagemagick
- created a thumbnail variant with imagemagic

```
  def thumbnail
    return self.main_image.variant(resize: '100x100')
  end  

in view
      <%= link_to (image_tag post.thumbnail, class:'img-responsive'), post_path(post) if post.main_image.attached? %>  

```
- added bootstrap 4
- added jquery
- added images to posts with active storage
- added comments with javascript no page refresh
- added ability to delete comments with javascript no page refresh
- bootstrap alert helper in application helper

```
module ApplicationHelper
  def alert_for(flash_type)  
    { success: 'alert-success',
      error: 'alert-danger',
      alert: 'alert-warning',
      notice: 'alert-info'
    }[flash_type.to_sym] || flash_type.to_s
  end   
end
```
<hr>

