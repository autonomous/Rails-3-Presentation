!SLIDE

# Validation #
***

!SLIDE code smaller

    @@@ruby
    # Rails 2
    validates_presence_of :login
    validates_length_of :login, :minimum => 4
    validates_uniqueness_of :login
    validates_format_of :login, :with => /[A-Za-z0-9]+/

***
    
    @@@ruby
    # Rails 3
    validates( :login, 
      :presence => true, 
      :length => {:minimum => 4},
      :uniqueness => true, :format => { :with => /[A-Za-z0-9]+/ }
    )
    
!SLIDE code

    @@@ruby
    :presence => true
    :uniqueness => true
    :numericality => true
    :length => { :minimum => 0, maximum => 2000 }
    :format => { :with => /.*/ }
    :inclusion => { :in => [1,2,3] }
    :exclusion => { :in => [1,2,3] }
    :acceptance => true
    :confirmation => true
    
!SLIDE

# It's easy to create custom validator types #
***

!SLIDE code smaller

    @@@ruby
    class ProperCategoryValidator < ActiveModel::EachValidator
      def validate_each(record, attribute, value)
        unless record.user.category_ids.include?(value)
          record.errors.add attribute, 'has bad category.'
        end
      end
    end
    
    ...
    # ... inside your model
    validate :category_id, :proper_category => true
    
!SLIDE
# ... or create validation classes #
***

!SLIDE code smaller

    @@@ruby
    class ReallyComplexValidator < ActiveModel::Validator
      def validate(record)
        record.errors[:base] << "This check failed!" unless thing(record)
        record.errors[:base] << "This failed!" unless other(record)
        record.errors[:base] << "FAIL!" unless fail(record)
      end

    private
      def thing(record)
        # Complex validation here...
      end

      def other(record)
        # Complex validation here...
      end

      def fail(record)
        # Complex validation here...
      end
    end

    # ... inside your model
    class NewsPost < ActiveRecord::Base
      validates_with ReallyComplexValidator
    end