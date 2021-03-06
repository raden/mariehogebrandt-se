#Terminology in Web Development
<summary>
Descriptions and definitions of words commonly (or not...) used.
</summary>

Words can be difficult, since their definition occasionally differs depending on the biases of the person who uses them. To at least try to minimise that, this is a catch-all page for terminology and how I use it. It shouldn't differ too much from the dictionaries (and Wikipedia), but with more examples so we are on the same page.

## 3-tier Architecture {#architecture}
For the more formal and broader (IE not just web development) definition, [Wikipedia has an article on 3-tier Architecture](http://en.wikipedia.org/wiki/Multitier_architecture), which is the basis for my definitions.

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

## Flat Build {#flat-build}
This is a term I picked up quite recently, when I was browsing around and found [Matt Bailey's](http://blog.mattbailey.co/post/52949597525/front-end-process-flat-builds-and-automation) articles on it, and it immediately resonated with me, so once I finally finish it there will be an article on how I implement it, but until then this definition will have to do. Oh, and also [David Bushell's](http://dbushell.com/2013/03/18/the-flat-build/) two articles that go a very different route from Matt Bailey.

What is it? Well, it is the description of developing the frontend independently of the backend, that is with pure HTML, CSS and JavaScript, using either mockup data or a fixed dataset of some kind.

Matt Bailey in his pieace speaks of [Assemble](http://assemble.io) which is based on [Handlebars](http://handlebarsjs.com/) templates, using [Grunt](http://www.gruntjs.com) to build HTML-pages, David Bushell [rolls his own](https://gist.github.com/dbushell/5186122). The big thing that both of them push (and that I adopted wholesale) is that having some kind of build system even for pure HTML, eases maintainability. The current HTML-mockups of my site looks nothing like the way the site does, because I changed something, and figured it was enough to test it in the `index.html` page.

It probably is a touch overkill occasionally, but by building the mockups using some kind of assembling system, it ensures that a change in one gets reflected in the others, and you can test that the JavaScript and CSS changing on one page doesn't break another.

## Cases {#cases}
Snake case, camel case, etc, etc, etc. What are they? Well, it's not always agreed on, but here's a starting list.

### Snake Case (or snake_case)

* Only lowercase letters (with the possible exception of the first letter)
* Words are separated with a single underscore
* Both Python and Ruby recommend snake case for non-constants and non-classes

### Camel Case (or Pascal Style)

* Each new word starts with a capital letter
* If the first letter is a capital it's referred to as UpperCamelCase (or StudlyCaps or CapWords), if it's a lowercase letter it's lowerCamelCase (or camelCase or mixedCase)
* .NET and JavaScript both encourage the use of Camel Case, with StudlyCaps denoting classes
* Ruby and Python recommend StudlyCaps for class names

### Hyphen-delimited

* Only lowercase letters
* Words are separated with a single hyphen
* [CSS is a hyphen-delimited syntax](http://csswizardry.com/2010/12/css-camel-case-seriously-sucks/)

### UPPER_CASE_WITH_UNDERSCORES (or SCREAMING_SNAKE_CASE)

* Only capital letters
* Words are separated with a single underscore
* Many languages/code styles recommends it for constants
    * Python - [Pep 8](http://www.python.org/dev/peps/pep-0008/#constants)
    * Ruby - [Ruby Style Guide](https://github.com/bbatsov/ruby-style-guide)
    * PHP - [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)
