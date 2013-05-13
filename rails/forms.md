### ->Rails forms notes <-

- `fields_for` can be used two ways. One in which it is called on a form builder object `<%= f.fields_for ... %>` and one in which it is called independing of a form builder `<%= fields_for ... %>`. In the latter case it passes the fields independent of the object attributes hash that might be existing in the `form_for` block that it might be nested in. 

- `accepts_nested_attribtues_for` basically generates `my_model_attributes=` within the model. When the form builder notices this, the parameters are appropriately passed as params[]

- It is not necessary to use `accepts_nested_attributes_for` if `my_model_attribtues=` is explicitly defined in the model

- Once we use `my_model_attributes=` or `accept_nested_attribtues_for` the form builder expects the object to be an ActiveRecord Object. 

- If you use `f.fields_for` without a corresponding `..._attributes=` method in the parent class, then the fields in the form will be passed inside the hash containing the attribtues of the parent object. These fields will not have the `_attributes` added to the the key of the hash. 


