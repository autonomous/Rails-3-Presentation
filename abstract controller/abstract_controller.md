!SLIDE

# AbstractController #

***

!SLIDE code smaller
    @@@ruby
    
    
    require 'abstract_controller'
    require 'action_dispatch'

    module ActionController
    ...
***
    @@@ruby
    
    require 'abstract_controller'
    require 'action_view'
    ...

    module ActionMailer
    ...
    
!SLIDE code smaller

    @@@ruby
    # AbstractController handles the basic notion of controllers,
    # actions, and action dispatching, and not much else.
    require 'abstract_controller'
    require 'action_dispatch'

    module ActionController
    ...
***
    @@@ruby
        
    require 'abstract_controller'
    require 'action_view'
    ...

    module ActionMailer
    ...
    
!SLIDE code smaller

    @@@ruby
    # AbstractController handles the basic notion of controllers,
    # actions, and action dispatching, and not much else.
    require 'abstract_controller'
    require 'action_dispatch'

    module ActionController
    ...
***
    @@@ruby
    # ... which is separated from the idea of HTTP
    require 'abstract_controller'
    require 'action_view'
    ...

    module ActionMailer
    ...

!SLIDE code

    @@@ruby
    module AbstractController
      extend ActiveSupport::Autoload
      
      autoload :Base
      autoload :Callbacks
      autoload :Collector
      autoload :Helpers
      autoload :Layouts
      autoload :Logger
      autoload :Rendering
      autoload :Translation
      autoload :ViewPaths
    end