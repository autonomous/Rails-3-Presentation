!SLIDE

# ActionMailer #
***

!SLIDE code smaller

    @@@ruby
    # Rails 2.3 - TMail implementation

    class Notifier < ActionMailer::Base
      def signup_notification(recipient)
        recipients      recipient.email_address_with_name
        subject         "New account information"
        from            "system@example.com"
        content_type    "multipart/alternative"
        body            :account => recipient

        part :content_type => "text/html",
          :data => render_message("signup-as-html")

        part "text/plain" do |p|
          p.body = render_message("signup-as-plain")
          p.content_transfer_encoding = "base64"
        end

        attachment "application/pdf" do |a|
          a.body = generate_your_pdf_here()
        end

        attachment :content_type => "image/jpeg",
          :body => File.read("an-image.jpg")

      end
    end
    

!SLIDE code smaller

    @@@ruby
    # Rails 3 - Now with Mail
    
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

!SLIDE

# Sending Mail

!SLIDE code smaller

    @@@ruby
    # Rails 2.3
    Notifier.deliver_signup_notification(recipient)

***

    @@@ruby
    # Rails 3
    Notifier.signup_notification(recipient).deliver

!SLIDE code smaller
    
    @@@ruby
    # Rails 2.3
    message = Notifier.create_signup_notification(recipient)
    Notifier.deliver(message)
    
***

    @@@ruby
    # Rails 3
    message = Notifier.signup_notification(recipient)
    message.deliver
    
!SLIDE

# GMail config #

***
    
!SLIDE code

    @@@ruby
    # config/application.rb
    ActionMailer::Base.delivery_method = :smtp
 
    ActionMailer::Base.smtp_settings = {
      :enable_starttls_auto => true,
      :address => 'smtp.gmail.com',
      :port => 587,
      :domain => "yourdomain.com",
      :user_name => 'administrator@yourdomain.com',
      :password => 'cisforcookie',
      :authentication => 'plain',
    }