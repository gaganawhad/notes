- A pattern to memoize a block of code that could return several values is<sup>1<sup>: 
  ```ruby 
  @main_address ||= begin
    maybe_main_address = home_address if prefers_home_address?
    maybe_main_address = work_address unless maybe_main_address
    maybe_main_address = addresses.first unless maybe_main_address
  end
  ```
  
- Here is how you would cache a method with parameter<sup>1</sup>: 
  ```ruby
  def self.top_cities(order_by)
    @top_cities ||= Hash.new do |h, key|
      h[key] = where(top_city: true).order(key).to_a
    end
    @top_cities[order_by]
  end
  ```

- An uglier but better pattern to memoize is: 
  ```ruby
    return @twitter_followers if defined? @twitter_followers
    @twitter_followers = twitter_user.followers 
  ```
  as compared with: 
  
  ```ruby
    @twitter_followers ||= twitter_user.followers
  ```
  
  The former allows for nil and false to be a legit memoized return values.<sup>1</sup> 
  
References: 

- 1http://www.justinweiss.com/blog/2014/07/28/4-simple-memoization-patterns-in-ruby-and-one-gem/
