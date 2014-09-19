# irl #

DDD supporting Integrated Requirements Language

IRL has:

* The IRL Statements
* The domain
* The executor

## IRL Statements ##

IRL Statements define the requirements that a product should do. Examples of
such statements in hypotheses format:

* If I have a cog then the cog should have a widget
* If I make a cog then I should be able to delete it
* If I do not have a cog then I cannot have a widget

Or similar things in declarative format:

* Create a cog then delete it. The cog should be gone.
* Create a cog with a widget. Delete the widget. The cog should still exist.

## The Domain ##

The domain defines what IRL is talking about. This is the domain specific 
language (DSL) that the IRL statements are to be parsed on.

The domain consists of:

* Nouns and their relationships
* Adjectives
* Verbs
* Actors
* Conditionals

### Parsing a statement ###

Given the statement:

* Create a cog with a widget then delete it. The cog should be gone.

The breakdown, using REST-JSON executor, is as follows:

* *Create* (verb)
  
        Expects a noun or nouns and will translate to POST.

* *a* (ordinal)
  
        'a' is a singular, equivalent to 1, one, 'a single', etc.

* *cog* (noun)

        A noun that create will be executed on and translates to the API
        resource for a cog, such as /v1.0/cogs.

* *with* (relationship)
* *a* (ordinal)
  
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
* *The* (probably ordinal?)
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

* NOOP executor: will output information
* REST-JSON: will perform REST calls to provided API with particular auth info
