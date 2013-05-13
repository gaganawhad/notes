### Rails forms notes

- `fields_for` can be used two ways. One in which it is called on a form builder object `<%= f.fields_for ... %>` and one in which it is called independing of a form builder `<%= fields_for ... %>`. In the latter case it passes the fields independent of the object attributes hash that might be existing in the `form_for` block that it might be nested in. 

- `accepts_nested_attribtues_for` basically generates `my_model_attributes=` within the model. When the form builder notices this, the parameters are appropriately passed as params[]

- It is not necessary to use `accepts_nested_attributes_for` if `my_model_attribtues=` is explicitly defined in the model

- Once we use `my_model_attributes=` or `accept_nested_attribtues_for` the form builder expects the object to be an ActiveRecord Object. 

- If you use `f.fields_for` without a corresponding `..._attributes=` method in the parent class, then the fields in the form will be passed inside the hash containing the attribtues of the parent object. These fields will not have the `_attributes` added to the the key of the hash. 


-------
#### some code to understand how fields_for works 

```erb
<%= form_for(@resource) do |f| %>
  .
  <%= fields_for :authors do |g| %> #NOTE this line
  .
<% end %>
```

```ruby
(rdb:22) p params["resource"]
{"title"=>"title #1", "content"=>"content #1"} ## Authors not nested

(rdb:22) p params["authors"]
{"name"=>"author #1"}

```
-------

```erb
<%= form_for(@resource) do |f| %>
 .
<%= f.fields_for :authors do |g| %> #NOTE this line
 .
<% end %>
```

```ruby
(rdb:40) p params['resource']
{"title"=>"title #2", "content"=>"content #2", "authors"=>{"name"=>"author #2"}} ## Nested Authors
```

----
When Authors model has associations and either of the following methods set up (Note that at this point Rails expects Author to be a persistent model):

```ruby
def authors_attributes= attributes
end
```
or 
```ruby
accepts_nested_attributes_for :authors
```

```erb
<%= form_for(@resource) do |f| %>
.
  <%= f.fields_for :authors do |g| %> #NOTE this line
.
<% end %>
```

```ruby
(rdb:82) p params['resource']
{"title"=>"title #3", "content"=>"content #3", "authors_attributes"=>{"0"=>{"name"=>"author #3"}}}
```

------

```erb
<%= form_for(@resource) do |f| %>
.
  <%= fields_for :authors do |g| %> #NOTE this line
.
<% end %>

```


```ruby
(rdb:90) p params['resource']
{"title"=>"title #4", "content"=>"content #4"}
(rdb:90) p params['authors']
{"name"=>"author #4"}
```



