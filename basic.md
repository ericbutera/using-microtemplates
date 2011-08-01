Micro-Templating with underscore.js
===================================

Recently I stumbled across an interesting way of working with markup in 
JavaScript applications: micro-templates.  In this post I will use the
words template and view interchangeably.

The Problem
-----------

Have you ever found yourself needing to inject some html into a page and 
started crafting something seemingly harmless like so:

    var html = "<ul>";
    for(var x=0; x < items.length; ++x){
      var item = items[x];
      html += "<li>" + item.name + "</li>";
    }

At first this got the job done, but later a revision is needed. Repeat 
several iterations of this and pretty soon all that is left is a mess 
of code and markup inside strings with escape codes all over.  We've all 
been there and fallen victim to these abominations.  In all our other
code we go through stringent pains to adhere to paradigms like MVC or
Template View.  Why should JavaScript be any different?


A Solution
----------

Let's start off with one of those banal examples that makes a person
question whether the subject is a worthwhile endeavor.  (I'm looking at you 2,500 
line OOP Hello World introductions.)  Our first task: create a prompt for a 
user's name and render it back using an underscore.js template.

    <div id="welcome"></div>
    <form>
    <em>Exciting Markup!</em>
    <label for="name">Name please</label>
    <input name="name" id="name" value="Ishmael" />
    <input type="button" id="welcome-action" value="Click for a surprise" />
    </form>

Now we create a little template that underscore can use template.  This will be 
inline in our basic demo.  More advanced usage can send these over the wire.

    <script type="text/html" id="welcome-tpl">
    <em>Exciting Template!</em>
    <strong >Hello <%= name %></strong>
    </script>

Progress!  Next up we'll need some quick and messy JavaScript wiring
using jQuery and underscore.js.  There are various other micro-template
plugins specifically for jQuery, but I have really grown to enjoy using
all of the wonderful tools available in underscore.js.

    var greet = _.template($("#welcome-tpl").text());
    $("#welcome-action").click(function(){
        var html = greet({'name': $("#name").val() });
        $("#welcome").html(html);
    });

The above snippet compiles the underscore template into the identifier
greet.  It gets the data from the welcome-tpl script tag which is most
beautiful part - we can now easily separate markup from code.  The final
part is calling greet with json to fill in the view variables.

This demo is hopefully straight forward.  The workflow boils down like
so:
 -   create a form to gather name
 -   create a template inside a script tag that we can access
 -   use jQuery to watch for click to render our template with user input

In part two I'll walk through creating an application that will fetch
weather from a remote API and render it using templates and partials.

