[Rails 7: The Demo - YouTube](https://www.youtube.com/watch?v=mpWFrUwAN88)

## Setup 

### VSCode Setup

Install the following extension:
- ruby
- ruby solargraph
- endwise
- erb helper tags
- rails db schema
- ruby-rubocop

Add the following to settings
```
"emmet.includeLanguages": {
  "erb": "html"
},
```

### Rails setup

```bash

brew install rbenv ruby-build

rbenv install 3.0.3

rbenv global 3.0.3

gem install rails -v 7.0.0

rbenv rehash # put rails in executable path

rails -v # verify Rails 7.0.0

brew install postgresql

brew services start postgresql     # To have launchd start postgresql at login
```

## Youtube

### Scaffolding
(0.00)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=0s]

```bash
rails new demo

rails generate scaffold post title:string content:text
```

Take a look at:
- migration `..._create_posts.rb` 
- model `post.rb`
- controller `posts_controller.rb`
  - autogens 7 default REST actions
- ^ creates layouts e.g. `index.html.erb` 

```bash
rails db:migrate

rails server
```

go to `localhost:3000/posts` to view generates app
- create some test posts, play around

`application.html.erb` is the default layout

`posts_controller.rb`
- goto `localhost:3000/posts.json` to view autogen json
- In controller look at `format.json`

### Developing the Domain Model - Post
(4.00)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=240s]

Add a validation in `post.rb`
- `validates_presence_of :title`
- To edit the error message, look in `posts/_form.html.erb`

### Built in console/repl
(5.08)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=308s]

```bash
rails console
```

```ruby
Post.first
Post.create! title: "From the console", content: "Nice!"
Post.all
Post.where(created_at: Time.now.all_day).to_sql
Post.where(created_at: Time.yesterday.all_day).to_sql
```

```bash
rails action_test:install
bundle install  # to install image gem
```

### ActionText Rails' Rich Text Editor
(6.15)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=375s]

In model
```ruby
has_rich_text :content
```

```ruby
<%= form.rich_text_area :content %>
```

ActionText allows rich text and even file/image uploads

### Javascript Import Maps - no node or webpack .D
(9.20)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=560s]

Looking at `application.js` you see ActionText doesn't require additional JS.
Includes `hotwired/turbo-rails`

### Adding JS packages using pins
(10.25)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=625s]

To add additional JS, we can...
```bash
./bin/importmap pin local-time
```

Now we can use 
```ruby
<%= time_tag post.created_at, "data-local", "time-ago" %>
```

We can now use JS without node

### Downloading JS packages instead of using CDN
(12.50)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=770s]

To vendor lock JS
```bash
./bin/importmap pin local-time --download
```

### Adding Comments to the Blog Post
(13.40)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=820s]

Instead of creating a complete scaffold, we can use lightweight `resource` instead
```bash
rails g resource comment post:references content:text
```

`post:references` sets up comment `belongs_to` Post, but we also need to add
`has_many :comments` to `post.rb`

To test...
```bash
rails console
```

```ruby
Post.first.comments.create! content: "First comment!"
```

### Adding Comments to the Web UI
(15.40)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=940s]

In `show.html.erb` for Posts, add a comments partial
```ruby
<%= render "posts/comments", post: @post %> 
```

Create `_comments.html.erb` and `_new.html.erb` and `_post.html.erb` 

*See code in video*

Also add `routes.rb`

See console to look at logs of routes/sql being called

### Adding Email Notifications with ActionMailer
(20.40)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1240s]

```bash
rails g mailer comments submitted
```

Pass in `comment` into `def submitted` in `comments_mailer.rb`

Set `mail to: ...`

See `views/comments_mailer` for templates

Mailer has an email preview

`CommentsMailer.submitted(comment).deliver_later)` to set up async messages

### Live Updates via Websockets
(24.20)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1460s]

Set up a *subscription* to a Turbo stream

In `show.html.erb`
```ruby
<%= turbo_stream_from @post %>
```

In `comment.rb`
```ruby
broadcasts_to :post
```

Updates to comments will now broadcast to Post. This works in UI or in console (ie by updating a comment in console)
```ruby
Post.find(3).comments.last.destroy
```

### Testing
(27.30)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1650s]

```bash
rails test
```

### Deploying to Heroku
(29.15)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1775s]

```bash
rails db:system:change --to=postgresql # since heroku uses pg
git add . & git commit -m "commit"
heroku create
git push heroku main
heroku run rake db:migrate
heroku addons:create heroku redis.hobby-dev -a <HEROKU-APP>
```

Set up root route in `routes.rb`
```ruby
root "posts#index"
```

## Code

###### :boat: [$ rails new demo](https://github.com/arafatm/rails.7.demo.dhh/commit/92792b2)

###### :boat: [$ rails generate scaffold post title:string content:text](https://github.com/arafatm/rails.7.demo.dhh/commit/b7639a8)
- [migration in `db/migrate/*_create_posts.rb`](https://github.com/arafatm/rails.7.demo.dhh/commit/b7639a8#diff-19bb1332c4dbbedb886ace81a246a896fb15f056b5fac81123df11824939b49b)
- [model in `app/models/post.rb`](https://github.com/arafatm/rails.7.demo.dhh/commit/b7639a8#diff-dcca05c4c31044a1b7ecb9bf3b861a09a7815486193bac57786acfa2d29eb034)
- [controller in `app/controllers/post_controller.rb`](https://github.com/arafatm/rails.7.demo.dhh/commit/b7639a8#diff-51479c7c729c095de9feb4e1243edad66f03be533b7237e3bde2250444e3e794)
  - 7 default actions, each with a view template
- [Views in `app/views/posts`](https://github.com/arafatm/rails.7.demo.dhh/tree/main/demo/app/views/posts)

xxx
