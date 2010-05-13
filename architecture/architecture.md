!SLIDE smbullets
# What's new in the Rails architecture #
***
* Core components are decoupled
* ActiveModel
* AbstractController
* ActionMailer is cool now
* Arel
* Everything except MVC?

!SLIDE bullets incremental

# ActiveModel #
***
* ActiveModel API - the interface that models must adhere to in order to gain compatibility with ActionPack’s helpers
* ActiveModel modules - easily gain access to cool features (previously buried in yards of twine)

!SLIDE code small
# ActiveModel Modules: Validation
***
    @@@ruby
    class Person
      include ActiveModel::Validations

      validates_presence_of :first_name, :last_name
      
      attr_accessor :first_name, :last_name
      def initialize(first_name, last_name)
        @first_name, @last_name = first_name, last_name
      end

    end
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
    
!SLIDE bullets incremental small

# ActionMailer #
***
* Out with TMail
* In with... Mail
* new DSL

!SLIDE code smaller

# ActionMailer #
***
    @@@ruby
    class Notifier < ActionMailer::Base
      default :from => "system@example.com"

      def signup_notification(recipient)
        @account = recipient

        attachments['an-image.jp'] = File.read("an-image.jpg")
        attachments['terms.pdf'] = {:content => generate_your_pdf_here() }

        mail(:to => recipient.email) do |format|
          format.text { render :text => "This is text!" }
          format.html { render :text => "<h1>This is HTML</h1>" }
        end
      end
    end
    
!SLIDE code smaller

# ActionMailer #
***

    @@@ruby
    Notifier.signup_notification(recipient).deliver
    
## OR ##

    @@@ruby
    # returns a Mail object
    message = Notifier.signup_notification(recipient)
    message.deliver