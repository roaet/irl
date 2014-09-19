irl
===

DDD supporting Integrated Requirements Language

IRL has:

* The IRL Statements
* The domain
* The executor


IRL Statements
--------------

IRL Statements define the requirements that a product should do. Examples of
such statements:

* If I have a cog then the cog should have a widget
* If I make a cog then I should be able to delete it
* If I do not have a cog then I cannot have a widget


The Domain
----------

The domain defines what IRL is talking about. This is the domain specific 
language (DSL) that the IRL statements are to be parsed on.

The domain consists of:

* Nouns and their relationships
* Adjectives
* Verbs
* Actors
* Conditionals


The Executor
------------

The executor is an interface definition for the parser to use while parsing.

Examples of what the executor does:

* "Create a cog" will cause the executor to attempt to instantiate a cog
  object
* "Create a cog and read it" will cause the executor to attempt to instantiate
  a cog object and then retrieve its information


Executor Implementations
~~~~~~~~~~~~~~~~~~~~~~~~

As the executor is only an interface definition it must be implemented to do
anything. Planned executors are:

* NOOP executor: will output information
* REST-JSON: will perform REST calls to provided API with particular auth info
