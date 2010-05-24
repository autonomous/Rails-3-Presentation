!SLIDE
# Routes #
***

!SLIDE code

    @@@ruby
    # Rails 2.x
    ActionController::Routing::Routes.draw do |map| 
      map.resources :posts 
    end 
    
    # Rails 3.x - namespaced to your app
    AppName::Application.routes do
      resources :posts 
    end 

!SLIDE



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