# Start of developing/workflow
<summary>
    
</summary>

As a starting comment: This is a constant work in progress. I find something that doesn't work and replace it with something that does, add something else, remove something superfluous, slowly but surely trying to get to the point where I have a workflow that is sustainable and comfortable, and that makes it easy to work with, preferrably in a team (most of this has yet to be tested in a team).

## 3-tier Architecture
Words are occasionally difficult, since their definition occasionally differs depending on the biases of the person who uses them, but I will try to use [3-tier Architecture](http://en.wikipedia.org/wiki/Multitier_architecture) as close to that definition as possible, which gives the following:

### Front-end/User Interface/Presentation layer
What the browser renders. HTML, JavaScript, graphics, CSS. It can be quite simple, or advanced through use of more complex JavaScript applications, or for that matter CSS animations and such. The to me important matter is that it should be separated from data and, in particular, from whatever server-side languages are used. It should not be important to the UI whether this is a WordPress site written in PHP, or a Python site with (or without...) Django, or a Ruby on Rails application, or for that matter a fat client which gets the data using a REST adapter from "somewhere else" (I'm looking at you, Ember!).

It can (and probably often is) debated on whether templating languages such as Smarty or Blade belongs to the front-end, but I overall consider them separate from it, but using the standards developed by the front-end.

Another consideration is whether the admin areas would be part of the front-end, to which I say "absolutely!", at least from a developer perspective. There is very little difference between building a UI (to use that part of the front-end) intended to show the latest cat images to any one who wants to see them and building a UI that is intended to allow an author to upload their latest masterpiece, outside of complexity. It's expectations that the deeper layers of the stack should fulfill: If I do X then Y, if I do Z then A. This happens if I mouse over that, if I upload a valid file then it should be uploaded.

Forms and such should be validated in the front-end, but they should also be validated deeper in the stack, obviously.

### Middleware
This often gets referred to as "backend", my main reason to divide the terms has to do with testibility. This is where your server-side language of choice fits in, and it should serve the information in a way that the presentation layer can handle. That might be translating tables to a JSON object that is consumed by an Ember model, and/or generating the agreed-upon scripts/CSS/HTML that the presentation layer has developed. Generally, if one uses/develops for WordPress, this is about as deep in the stack as one gets. 

As a note, if you've ever played on role playing chats, most of what is referred to as "the database" is in this layer, the misnomer having to do with confusing the stored characters/data and the presentation of said characters/data. This layer communicates with the actual data storage, but it should not be dependent upon one particular type of it. In reality it's impractical to build something that could be easily changed from using, say, MySQL to NoSQL, but with a bit of carefulness it's at least possible to build something that doesn't need too much effort to move from a SQLite database (for development/testing) to a MySQL database (for production).

### Back-end/Persistence layer/Database
This should be the most secured part of the website. In an ideal world, you should not be able to access it (outside of dedicated areas on your webhost) through any other means than middleware, and there should be strict rules on how to interact with it.

How much effort goes into the database depends quite a bit on the kind of application, obviously. As I noted higher up, most people who develop in WordPress never really look into the database, and both Django, Laravel and Ruby on Rails (among others...) have ways to create tables and such without the developer needing to get their hands dirty with the functionalities of the data storage. 

However, the more important the data and its' structure is, the more important it is to take good care with the persistance layer. The larger the application, the higher the number of users and number of transactions, the more effort needs to be put into making it right to begin with, and very few Object-Relation Managers can deal with complex and large sets of data as efficiently as someone who knows exactly what needs to be done, and how to do it. Figuring out keys and indices and how much of a cell needs to be covered for the full-text search to perform well without being useless are all tasks better suited for people than for software. 

Personally, I would also add cron jobs and similar things to the description of back-end. They might use the same libraries/framework as the middleware, but any tasks intended to do things heavily on the server are back-end tasks.

## Scope
Now that I've waffled on some about the different parts of architecture, my focus in these articles is mainly on the front-end and middleware. I've done my share of back-end things, in particular when developing, and I know my way around MySQL (that example with how large an index should be to cover enough of the text without being a bottleneck in performance? Yep, been there, done that), but overall it's not what I do. I do web applications/sites.

## Preparations
I can not stress enough the importance of knowing not only _why_ you're wanting the site and what you're wanting to accomplish with it, but also to have a clear view of what it will offer. This is not a place to figure out colours and layout and how to implement the parsing of uploaded zipfiles, but to figure out the functionality. Cowboy coding comes in a lot of forms, figuring out the "what" as you're working on the "how" is one of the more common ones in smaller teams.
