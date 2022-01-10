[Rails 7: The Demo - YouTube](https://www.youtube.com/watch?v=mpWFrUwAN88)

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

xxx


