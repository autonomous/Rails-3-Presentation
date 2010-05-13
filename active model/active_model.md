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