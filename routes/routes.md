!SLIDE
# Routes #
***

!SLIDE code small

    @@@ruby
    # Rails 2
    ActionController::Routing::Routes.draw do |map| 
      ...
    end 
***
    @@@ruby    
    # Rails 3 - namespaced to your app
    AppName::Application.routes do
      ...
    end 

!SLIDE code small

    @@@ruby
    match ':controller(/:action(/:id(.:format)))'
    
***    

    @@@ruby
    # login_url or login_path
    match '/login' => 'accounts#login', :as => 'login'
    
***    

    @@@ruby
    # root_url or root_path
    root :to => 'blogs#index'

!SLIDE code smaller

    @@@ruby
    # http://localhost:3000/articles/2005/11/06
    # maps to
    # params = {:year => '2005', :month => '11', :day => '06'}
    match '/articles/:year/:month/:day', :constraints => {
      :controller => 'articles',
      :action => 'find_by_date',
      :year => /\d{4}/,
      :month => /\d{1,2}/,
      :day => /\d{1,2}/
    }

!SLIDE code smaller

    @@@ruby
    # Rails 2
    map.resources( :forums, 
        :collection => { :sortable => :get, :sort => :put }
        ) do |forums|
      forums.resources :topics
    end
***
    @@@ruby
    # Rails 3
    resources :forums do
      collection do
        get :sortable
        put :sort
      end
      resources :topics
    end

!SLIDE
## Generic redirecting in Rails 2.3 ##
***

!SLIDE code smaller

    @@@ruby
    # Controller
    class GenericController < ApplicationController
      def redirect
        redirect_to(params[:url] % params, params[:options])
      end
    end
    
    # In your routes file
    map.connect "/foo/:id", :controller => "generic", \
      :action => "redirect", :url => "/bar/%{id}s"

!SLIDE
## Generic redirecting in Rails 3 ##

!SLIDE code small

    @@@ruby
    match "/foo/:id", :to => redirect("/bar/%{id}s")

!SLIDE

## What does the source code look like? ##

!SLIDE code smaller

    @@@ruby 
    def redirect(*args, &block)
      options = args.last.is_a?(Hash) ? args.pop : {}

      path = args.shift || block
      path_proc = path.is_a?(Proc) ? path : proc {|params| path % params }
      status = options[:status] || 301

      lambda do |env|
        req = Rack::Request.new(env)
        params = path_proc.call(env["action_dispatch.request.path_parameters"])
        url = req.scheme + '://' + req.host + params
        [
          status, 
          {'Location' => url, 'Content-Type' => 'text/html'}, 
          ['Moved Permanently']
        ]
      end
    end
    
!SLIDE center

##  New Routes DSL  ##
***

!["Every endpoint is essentially a Rack application"](rack-logo.png)

### "Every endpoint is essentially a Rack application" ###
> http://www.railsdispatch.com/posts/rails-routing

!SLIDE code small

    @@@ruby
    class CookieMonsterApp < Sinatra::Base

      get '/'
        "Me want cookie!"
      end

      get '/eat'
        "Om NOM NOM NOM"
      end

    end

    match '/cookies' => CookieMonsterApp

!SLIDE bullets

* Ramaze
* Camping
* Merb