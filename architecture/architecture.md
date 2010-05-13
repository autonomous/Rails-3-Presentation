!SLIDE smbullets incremental
# What's new in the Rails architecture #

* Core components are decoupled
* ActiveModel
* AbstractController
* ActionMailer is cool now
* Arel
* Everything except MVC?

!SLIDE bullets



!SLIDE code smaller

# ActionController::Base #

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