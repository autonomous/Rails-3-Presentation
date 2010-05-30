!SLIDE

# Firing up a new app #
***

!SLIDE commandline incremental

    $ rails rails3_blog -d mysql

    $ rails server

!SLIDE

# Configuring your app #

***

!SLIDE code small

    @@@ruby
    # config/applicaiton.rb
    ...
    config.generators do |g|
      g.orm             :active_record
      g.template_engine :erb
      g.test_framework  :test_unit, :fixture => true
    end
    ...
    
!SLIDE

# Bundler is the new config.gem
***

!SLIDE code smaller

    @@@ruby
    # Edit this Gemfile to bundle your application's dependencies.
    source 'http://gemcutter.org'

    gem "rails", "3.0.0.beta"

    ## Bundle edge rails:
    # gem "rails", :git => "git://github.com/rails/rails.git"

    gem "mysql"

    ## Bundle the gems you use:
    # gem "bj"
    # gem "hpricot", "0.6"
    # gem "sqlite3-ruby", :require => "sqlite3"
    # gem "aws-s3", :require => "aws/s3"

    ## Bundle gems used only in certain environments:
    # gem "rspec", :group => :test
    # group :test do
    #   gem "webrat"
    # end

!SLIDE commandline smaller

    $ rails generate scaffold post title:string body:text
    invoke  active_record
    create    db/migrate/20100202054755_create_posts.rb
    create    app/models/post.rb
    invoke    test_unit
    create      test/unit/post_test.rb
    create      test/fixtures/posts.yml
     route  resources :posts
    invoke  scaffold_controller
    create    app/controllers/posts_controller.rb
    invoke    erb
    create      app/views/posts
    create      app/views/posts/index.html.erb
    create      app/views/posts/edit.html.erb
    create      app/views/posts/show.html.erb
    create      app/views/posts/new.html.erb
    create      app/views/posts/_form.html.erb
    create      app/views/layouts/posts.html.erb
    invoke    test_unit
    create      test/functional/posts_controller_test.rb
    invoke    helper
    create      app/helpers/posts_helper.rb
    invoke      test_unit
    create        test/unit/helpers/posts_helper_test.rb
    invoke  stylesheets
    create    public/stylesheets/scaffold.css
