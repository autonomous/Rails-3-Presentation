!SLIDE bullets incremental

# ActionController #
***

* ActionDispatch
* AbstractController

!SLIDE bullets

# ActionDispatch #
***

* Request
* Response
* Mime type handling
* Middleware and Integration Test support
  
!SLIDE bullets

# AbstractController #
***
* Includes the concept of controllers, rendering, layouts, helpers, and callbacks
* Nothing about HTTP or mail delivery

!SLIDE code smaller

    @@@ruby
    # Rails 2.3
    class UsersController < ApplicationController
      def index
        @users = User.all
    
        respond_to do |format|
          format.html
          format.xml { render :xml => @users }
        end
      end

      def create
        @user = User.new(params[:user])

        respond_to do |format|
          if @user.save
            flash[:notice] = "User was successfully created"
            format.html { redirect_to @user }
            format.xml  { render :xml => @user, :status => :created, :location => @user }
          else
            format.html { render "new" }
            format.xml  { render :xml => @user.errors, :status => :unprocessable_entity  }
          end
        end
      end
    end

!SLIDE code smaller

    @@@ruby
    # Rails 3
    class UsersController < ApplicationController
      respond_to :html, :xml

      def index
        @users = User.all
        respond_with @users
      end

      def create
        @user = User.new(params[:user])
        flash[:notice] = "User was successfully created" if @user.save
        respond_with @user
      end
    end

!SLIDE 

# respond_with #
***
The respond_with method is a simple wrapper to an object called responder. A responder is any object that responds to call and receives the current controller and the given resource as parameters.

!SLIDE bullets incremental

# And this is cool because...? #
***

* Change behaviour in one place
* We can extend the responder behaviour
* Suggestions?

!SLIDE code smaller

# ActionController::Base #
***
    @@@ruby
    module ActionController
      
      class Base < Metal
        
        ...
        
        MODULES = [
          AbstractController::Layouts,
          AbstractController::Translation,

          Helpers,
          HideActions,
          UrlFor,
          ...
        ]

        MODULES.each do |mod|
          include mod
        end
        
        ...
        
    end
    
!SLIDE code smaller

# ActionController::Base #
***
    @@@ruby
    module ActionController
      # You could create your own controllers by inheriting Metal
      class Base < Metal

        ...
        
        MODULES = [
          AbstractController::Layouts,
          AbstractController::Translation,

          Helpers,
          HideActions,
          UrlFor,
          ...
        ]

        MODULES.each do |mod|
          include mod
        end

        ...

    end
    
!SLIDE code smaller

# ActionController::Base #
***
    @@@ruby
    module ActionController
      # You could create your own controllers by inheriting Metal...
      class Base < Metal

        ...
        # ... and simply picking the components you need
        MODULES = [
          AbstractController::Layouts,
          AbstractController::Translation,

          Helpers,
          HideActions,
          UrlFor,
          ...
        ]

        MODULES.each do |mod|
          include mod
        end

        ...

    end
    
!SLIDE code smaller

    @@@ruby
    AbstractController::Layouts,
    AbstractController::Translation,
    Helpers,
    HideActions,
    UrlFor,
    Redirecting,
    Rendering,
    Renderers::All,
    ConditionalGet,
    RackDelegation,
    SessionManagement,
    Caching,
    MimeResponds,
    PolymorphicRoutes,
    ImplicitRender,
    Cookies,
    Flash,
    RequestForgeryProtection,
    Streaming,
    RecordIdentifier,
    HttpAuthentication::Basic::ControllerMethods,
    HttpAuthentication::Digest::ControllerMethods,
    HttpAuthentication::Token::ControllerMethods,
    Instrumentation,
    AbstractController::Callbacks,
    Rescue