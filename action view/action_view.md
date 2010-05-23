!SLIDE

# ActionView #
***
<!-- Clear separation between ActoinController and ActionView -->
* ActionView exposes a __single API entry point__ for rendering templates and partials

!SLIDE

## It's faster ##
***

!SLIDE bullets

* Template lookups is faster
* Rendering Partial collections is much faster

!SLIDE bullets
## XSS protection ##
***

!SLIDE code smaller
    
    @@@ruby
    = form_for @person do |f|
      content_tag(:h1) do
        = @person.title
      end
      = f.label :name, "Name"
      = f.text_field :name
      = f.label :profile, "Profile"
      = f.text_area :profile
      = f.submit
    end
***
    @@@html
    <form action="/posts" method="post">
      <h1>&lt;script&gt;more evil content here&lt;/script&gt;</h1>
      <label for="person_name">Name</label>
      <input type="text" name="person[name]" \
        id="person_name" value="Darth Vader" />
      <label for="person_profile">Profile</label>
      <textarea name="person[profile]" id="person_profile">
        &lt;script&gt;some evil content here&lt;/script&gt;
      </textarea>
      <input type="submit">Create</input>
    </form>

!SLIDE code

    @@@ruby
    # Mark html as safe in your helpers
    "<div>#{snatch_cookie}</div>".html_safe

    # Manually un-escape html in your views 
    raw( @user.description )


!SLIDE
## HTML5 &  Unobtrusive JavaScript helpers ##
***

!SLIDE code

    @@@ruby
    = form_for @post, :remote => true do |f|
***
    @@@html
    ...
    ...  
    ...
    ...
    ...
    ...
    
!SLIDE code

    @@@ruby
    = form_for @post, :remote => true do |f|
***
    @@@html
    <form 
      action="http://host.com"  
      id="create-post"  
      method="post"  
      data-remote="true">
    ...

!SLIDE center
##  Core team maintains Prototype and jQuery drivers!  ##
***

![Supported JS drivers](javascript_drivers.png)

!SLIDE code small
    @@@ruby
    # inside config/initializers/jquery_init.rb
    ActionView::Helpers::AssetTagHelper.
      register_javascript_expansion(
        :jquery => %w/jquery jquery-ui rails application/
      )
      
    # inside your layout
    javascript_include_tag :jquery

