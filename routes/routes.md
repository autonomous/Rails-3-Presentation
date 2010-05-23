!SLIDE
# Routes #
***

!SLIDE center

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

