- Struct can be used to create a class <sub>1</sup>: 

  ```ruby
  class Customer
    # Internal: Class to create credit card value objects
    CreditCard = Struct.new(:holder, :type, :number)
    attr_reader :full_name, :card

    def initialize(full_name, card_type, card_number)
      @full_name = full_name
      @card = CreditCard.new(full_name, card_type, card_number)
    end
  end
  ```
  
  Advantages: 
  - Equality will be based on values 
  
  ```ruby
  customer1 = Customer.new('Thuva Tharma', 'visa', 1234)
  customer2 = Customer.new('Thuva Tharma', 'visa', 1234)
  customer3 = Customer.new('Thuva Tharma', 'amex', 1234)

  customer1 == customer2 #=> true
  customer1 == customer3 #=> false
  ```

  Disadvantage: 
  We lose arity check: 
  
  ```ruby
  # full_name, card_type, card_number are all nil
  Customer.new

  # card_type, card_number are nil
  Customer.new('Thuva Tharma')

  # card_number is nil
  Customer.new('Thuva Tharma', 'visa')

  # full_name, card_type, card_number are all present
  Customer.new('Thuva Tharma', 'visa', 1234)
  ```
  

References: 
  1. http://techblog.thescore.com/2014/07/19/3-ways-to-create-classes-in-ruby/
