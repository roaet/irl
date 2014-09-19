# irl #

Introspective Requirements Language supports Domain Driven Design.

IRL has:

* The IRL:Domain Defining Dialect
* The IRL:Requirement Defining Dialect
* The executor

## IRL Statements ##

The IRL Langauge defines the domain as well as the requirements of that domain.

### Domain Defining (DD) Dialect ###

The Domain Defining dialect defines what IRL is talking about.

The domain consists of:

* Nouns and their relationships
* Adjectives
* Verbs
* Actors
* Conditionals

The following examples of DD statements use a shortcut `CRUD` to define the
capabilities of the nouns (cog, widget) while simultaneously defining the
corresponding adjectives (created: create; deleted: delete):

* A cog can be CRUD
* Networks may contain widgets
* A subnet can be CRUD

The 2nd statement is forward declaration of a noun, `widgets` which is then
resolved on the next statement.

### Requirement Defining Statements ###

The Requirement Defining (RD) dialect defines the requirements that a product
should exhibit. Examples of such statements in hypotheses format:

* If I have a cog then I should be able to add a widget to it
* If I make a cog then I should be able to delete it
* If I do not have a cog then I cannot have a widget

Or similar things in declarative format:

* Create a cog then delete it. The cog should be gone.
* Create a cog with a widget. Delete the widget. The cog should still exist.

Finally there is natural format:

* I have a cog with a widget. I should be able to delete the cog and the widget
  should be deleted.

### Parsing a statement ###

Given the statement:

* Create a cog with a widget then delete it. The cog should be gone.

The breakdown, using REST-JSON executor, is as follows:

* *Create* (verb)
  
        Expects a noun or nouns and will translate to POST.

* *a* (cardinal)
  
        'a' is a singular, equivalent to 1, one, 'a single', etc.

* *cog* (noun)

        A noun that create will be executed on and translates to the API
        resource for a cog, such as /v1.0/cogs.

* *with* (relationship)
* *a* (cardinal)
  
        'a' is a singular, equivalent to 1, one, 'a single', etc.

* *widget* (noun)

        A noun that create will be executed on and translates to the API
        resource for a widget, such as /v1.0/widgets.

* *then* (action separation)
* *delete* (verb)
  
        Expects a noun or nouns and will translate to DELETE.

* *it* (specialized noun)
  
        Within a statement 'it' selects the most significant noun first which
        is the cog in this case.

* *.* (action separation)
* *The* (probably cardinal?)
* *cog* (noun)
* *should* be (conditional)
* *gone* (adjective)
  
        Translates to an expected 404 on GET for that resource which is a GET
        on /v1.0/cogs/id.

## The Executor ##

The executor is an interface definition for the parser to use while parsing.

Examples of what the executor does:

* "Create a cog" will cause the executor to attempt to instantiate a cog
  object
* "Create a cog and read it" will cause the executor to attempt to instantiate
  a cog object and then retrieve its information

### Executor Implementations ###

As the executor is only an interface definition it must be implemented to do
anything. Planned executors are:

* NOOP: will output information which is useful for checking IRL statement
  validity
* REST-JSON: will perform REST calls to provided API with particular auth info
* REST-Implement: will attempt to generate a RESTful API that will satisfy the
  given requirements

## Dependencies ##

IRL heavily leverages the pyparsing module.
