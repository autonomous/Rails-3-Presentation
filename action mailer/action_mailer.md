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