### DHH
- "Bad features came when I wanted a good framework. Good features came when I was solving my own problems" - DHH (_paraphrased_)


client vs rails
what criteria can we use to make thise decisions. 

where does the heart of your applicaiton live? is it a client interaction? may be is it mostly a interactino or is it mostly a consmpution? 

- uts not clear tha one side or the ohter side requires less code

both approches claim speed 

client side interaction is proporational to new data requirements. 

- speed of server is redued drastically when the internet is slow. 

- 

server style is optimized for least disruption to rails. 



Questions to ask when deciding the archietechture of the app. 

- is the representation of data stable ? (do different users see different thigns? ) 
- is interation with the server primarily notification? example a todo list. (example, updating a todo list - update the todo list on the client side and then tell server that you did it). 
- do client components interact? example maps. ember is really good at that. 
- what do you already have ? if you have rails developer, use rails developer 


### magic tricks of testing.


- just delete some tests. (writing too many tests can be bad)

unit test : Goas (its not about integration testign)
(every cell works correctly) integration tests( the beast is alive).

we need them to bte 
throughugh
stable 
fast 
few. 


focus on messages. 

- thre are incoming messages and the outside messages, and somemessages the object sent to itself. they are invisible to objects outside. 
- messages cane be a query or a command. 
- query messages don't have side affect. 
- command mesages return nothing and change something. 

- if we conflate commands and euresi then its a peril. 

- hidden side effects are the bane of our progammers
- queries and commands or (command and queries) get tested differently. 

- test incoming query messages by making assertings about what they send back. 
- you want to test the interface not the impelmentation. which means you shouldnt' be testing private methods. 


testing queries: 

- you make an aserction about the _direct public side effects_ 


messages sent to self. 

- thes test for private methods is redundnt. 

- you want to TEST API!!!!!!!! not the internals of a model. they will lock you down!!!!

- break rules if it saves $$$$$

- ignore messages sent to self. 

- outoging messages

- dot test outgoign query messages. do not make asserations about their result, do not expect to send them. 

      


 designing great apis. 

 - 
3 levesls
geroge orwell - writing
dieter rams - industrial design

kano model - product


orwell best knwon of novles. wrote esseays olicitcs and the english language. 

bad writing is a key to propaganda. 


five guiding principles: 

1. minimalism. keep the default case as simple of as possible
2.a good api design will get outof the way - you don't notice it. Example REST. 


dieter rams: 

you want to design for the extremes - for the edge cases - then the middle will take care of it self. 
- 
- makes api understandable



if service is unavaiable it should be unavailable



- good design is umobstrusive. 

- version your api. 

- good design is a l little design as possible. 

- good design is predictable. 


kano model: 

noriakoi kano

basic needs: 

- excite users. 



- 
why NoSQL


= look into marhsall. 
- loo into rss ways of solivng updated at. issues. also conditional get and google pushpull:w

-
posgres






### Managing the `lib/` directory

- namespace everything that is going in the lib directory
- Don't autoload the lib directory in your rails configuration!!! Add the `require` statements in the lib files
- Use DCI in lib... use role as mixin (Not sure how though)


### How a request becomes a response

- A webserver delivers web pages on the request of clients using http. It handles the delivery of the application content. 
- What an app server does is handles execution of processors. The app server is going to initialize rails. Example passenger / thin / mongrel (confirm the last two in this list)



#### maintable templates - loudermilk

- reasons: 
        - markup repetition
        - logic in templates


- logic in templates is supposed to be difficult to test


- while hepers are sueful, bug projects end up with tons of hlelpers.  they are difficult to organize. complex logic isn't well suited for them. some peopel like to do it on the model. 

- use decorator pattersn

wraps a slinge object
transparent interfeace - overlaps the 
forward methods to original object. 

add s presentationsl logc to modesl 


intitalize - method take the object you want to decorate. 

if something is direclty related to a model, it should be put in the decorator. 


use draper



complex views - connected wth user expereicnes 

example some code to remove names of participatns of a 


Presentation model: 




to initialize the presentation model, use a holepr.

Form builders are aan example of this. 

look into gems simple_forms / table_cloth


puts view presenations classes in lib


if its something that would go into a helper then it should go into a view object


cells gem - take a look at it

github/bloudermilk


