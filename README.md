# What is this

This is a very random side-project of mine. It is supposed to be a resource for tracking tasks of some software project.

# How does it work

The are several modules of the solutions, that make up the solution:

* Web server -- queries task storage and processes API requests
* Task storage -- stores the tasks and returns them from query
* Task widgets -- a bunch of plugins that allow rendering custom widgets inside the tasks

## More details

When a user requests a task the following happens:

1. The web server receives a request
2. The web server fetches the description from the storage
3. The web server invokes the widget plugins as it parses the description

## Plugin architecture

* A widget plugins are supposed to be a set of stateless functions: `model`, `head_view` and `view`
* When rendering the task page, the server does two passes over the description:
  1. The plugins build up their model values as the parser walks through the description (`model`).
  2. During the second pass, the web server renders the page for the task. Each plugin can instruct the server to replace some of the tokens with their own (`view`).
* A widget can also ask the server to add some stuff at the top of the task page (`head_view`).
