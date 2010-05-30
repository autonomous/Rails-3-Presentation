!SLIDE smbullets incremental

# ActiveModel #
***
* ActiveModel modules - easily gain access to cool features (previously buried in yards of twine)
* ActiveModel API - the interface that models must adhere to in order to gain compatibility with ActionPack’s helpers

!SLIDE

# ActiveRecord style validation

***

!SLIDE code small

    @@@ruby
    class Person
      

      

      
    
      def initialize(first_name, last_name)
        @first_name, @last_name = first_name, last_name
      end

    end
    
!SLIDE code small

    @@@ruby
    class Person
      

     

      attr_accessor :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name, @last_name = first_name, last_name
      end

    end
    
!SLIDE code small

    @@@ruby
    class Person
      include ActiveModel::Validations

      

      attr_accessor :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name, @last_name = first_name, last_name
      end

    end
    
!SLIDE code small

    @@@ruby
    class Person
      include ActiveModel::Validations

      validates_presence_of :first_name, :last_name

      attr_accessor :first_name, :last_name

      def initialize(first_name, last_name)
        @first_name, @last_name = first_name, last_name
      end

    end
    
!SLIDE commandline

    $ a_peep = Person.new( 'Fibby' )
    ...
    
    $ a_peep.valid?
    false
    
    $ a_peep.errors
    ...
    
!SLIDE code small
    @@@ruby
    AttributeMethods
    BlockValidator
    Callbacks
    Conversion
    DeprecatedErrorMethods
    Dirty
    EachValidator
    Errors
    Lint
    Name
    Naming
    Observer
    Observing
    Serialization
    TestCase
    Translation
    VERSION
    Validations
    Validator
    JSON
    Xml
    
!SLIDE 

# ActiveModel::Lint #

You can test whether an object is compliant with the ActiveModel API by
including ActiveModel::Lint::Tests in your TestCase. It will included
tests that tell you whether your object is fully compliant, or if not,
which aspects of the API are not implemented.

!SLIDE code 

    @@@ruby
    class NeverTest < Test::Unit::TestCase

      include ActiveModel::Lint::Tests
      ...
  
    end

!SLIDE

# Which gives you... #

!SLIDE code smaller

    @@@ruby
    ...
    def test_to_key
      # "The model should respond to to_key"
      assert model.respond_to?(:to_key), "The model should respond to to_key"
      def model.persisted?() false end
      assert model.to_key.nil?
    end

    def test_to_param
      # "The model should respond to to_param"
      assert model.respond_to?(:to_param), "The model should respond to to_param"
      def model.persisted?() false end
      assert model.to_param.nil?
    end
    ...