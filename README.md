ember-flows
===========

Easily build complicated route traversal patterns in Ember.


Reasoning
---------

We can distill any web application into exactly two constituent parts:

* Presenting information to the user for consumption.
* Collecting input from the user in order to mutate application state to achieve some purpose.

Input and output. Read and write. Nouns and verbs. Ember's goal has always been to make developers productive in accomplishing these tasks. The goal of ember-flows is to make that easy to accomplish when input from the user and application state mutations need to occur across multiple routes in your application.

### Locality & Encapsulation

You might say, "but this violates locality!" When you're building a series of routes which all need to be able to inspect a particular state in order to determine what is next, which is better:

a. Having every single route/controller bind in to the other controllers that may modify the state and may or may not be instantiated?
b. Having a single repository for the information necessary to traverse between routes?

Further, by splitting the progression through a process into multiple routes, you're creating better encapsulation for just that component of functionality. 

### What about child flows?

There are no such things. The only use case along these lines that ember-flows has plans to optimize for is where you can treat an entire flow as a single node. This use case applies most specifically to forcing a user to login in the middle of checkout. Until this functionality is available out of the box think of it as departing one flow (saving the state), passing a bit of information into the new flow (what to do when complete), and then returning to the previous flow.

### What if the flow's nodes are dynamically generated?

The most common example for this is a multi-step quiz application. Underneath the hood this is simply a self-referential traversal which will continue until some condition that means "completed" is saved in the flow, at which point it will follow the correct exit edge.


Implementation
--------------

Underneath the hood ember-flows is built using a directed graph. Nodes in the graph represent routes, and edges in the graph are decision points which are delegated to ember-flows. It's a state machine.


Tooling
-------

In a directed graph there are two possible representations: an adjacency matrix and an adjacency list. ember-flows uses an adjacency list. However, manually generating the adjacency list for your application is tedious and prone to error. Check out [ember-flows-generator](https://github.com/nathanhammond/ember-flows-generator) for an Ember application which can be used to generate the flows that you need for your application.