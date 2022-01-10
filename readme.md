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

# To have launchd start postgresql at login:
brew services start postgresql
```

## Youtube

### Scaffolding
(0.00)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=0s]

### Developing the Domain Model - Post
(4.00)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=240s]

### Built in console/repl
(5.08)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=308s]

### ActionText Rails' Rich Text Editor
(6.15)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=375s]

### Javascript Import Maps - no node or webpack .D
(9.20)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=560s]

### Adding JS packages using pins
(10.25)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=625s]

### Downloading JS packages instead of using CDN
(12.50)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=770s]

### Adding Comments to the Blog Post
(13.40)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=820s]

### Adding Comments to the Web UI
(15.40)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=940s]

### Adding Email Notifications with ActionMailer
(20.40)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1240s]

### Live Updates via Websockets
(24.20)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1460s]

### Testing
(27.30)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1650s]

### Deploying to Heroku
(29.15)[https://www.youtube.com/watch?v=mpWFrUwAN88&t=1775s]

## Practice

###### :boat: [$ rails new .](https://github.com/arafatm/rails.7.demo.dhh/commit/88eced3)

###### :boat: [$ rails generate scaffold post title:string content:text](https://github.com/arafatm/rails.7.demo.dhh/commit/49d3f91)
- `db/migrate/20220110023747_create_posts.rb`
- `app/models/post.rb`
- `app/controllers/posts_controller.rb`
- `app/views/posts/*.erb`

###### :boat: [$ rails db:migrate](https://github.com/arafatm/rails.7.demo.dhh/commit/a53195b)
- `db/schema.rb` to see current DB state

`$ rails server` to view app
- `http://127.0.0.1:3000/posts`

###### :boat: [stylin with simplecss](https://github.com/arafatm/rails.7.demo.dhh/commit/25c7828)

You can view json api with `localhost:3000/posts.json`. See the `format.html` vs `format.json` in `posts_controller.rb`

###### :boat: [validates_presence_of](https://github.com/arafatm/rails.7.demo.dhh/commit/a1b5a8f)

xxx


