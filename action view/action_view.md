!SLIDE

# ActionView #

!SLIDE bullets incremental

# ActionView #
***
* Major overhaul
* It's faster
* XSS protection
* Unobtrusive JavaScript helpers
* HTML5

!SLIDE smbullets incremental

# ActionView #
***
* Template lookups is faster
* Rendering Partial collections is much faster

<!-- Clear separation between ActoinController and ActionView -->

* ActionView exposes a __single API entry point__ for rendering templates and partials

!SLIDE code

# Less talk, more code!! #

!SLIDE code

# ActionView #
***
    @@@ruby
    form_for @post, :remote => true
***
    ...
    ...
    ...
    ...
    ...
    ...
    
!SLIDE code

# ActionView #
***
    @@@ruby
    form_for @post, :remote => true
***
    @@@html
    <form 
      action="http://host.com"  
      id="create-post"  
      method="post"  
      data-remote="true">
    ...
    
!SLIDE bullets incremental
# ActionView #
***

* HTML output is now escaped by default
* h( ... ) is now swimming with the fishes
* raw( ... ) if you want the un-escaped content
* Constant vigilance is for perl programmers...
    