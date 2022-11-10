Introduction
When developing a Ruby on Rails application, you may find you have application tasks that should be performed asynchronously. Processing data, sending batch emails, or interacting with external APIs are all examples of work that can be done asynchronously with background jobs. Using background jobs can improve your application’s performance by offloading potentially time-intensive tasks to a background processing queue, freeing up the original request/response cycle.

Sidekiq is one of the more widely used background job frameworks that you can implement in a Rails application. It is backed by Redis, an in-memory key-value store known for its flexibility and performance. Sidekiq uses Redis as a job management store to process thousands of jobs per second.

In this tutorial, you will add Redis and Sidekiq to an existing Rails application. You will create a set of Sidekiq worker classes and methods to handle:

A batch upload of endangered shark information to the application database from a CSV file in the project repository.
The removal of this data.
When you are finished, you will have a demo application that uses workers and jobs to process tasks asynchronously. This will be a good foundation for you to add workers and jobs to your own application, using this tutorial as a jumping off point.

Prerequisites
To follow this tutorial, you will need:

A local machine or development server running Ubuntu 18.04. Your development machine should have a non-root user with administrative privileges and a firewall configured with ufw. For instructions on how to set this up, see our Initial Server Setup with Ubuntu 18.04 tutorial.
Node.js and npm installed on your local machine or development server. This tutorial uses Node.js version 10.17.0 and npm version 6.11.3. For guidance on installing Node.js and npm on Ubuntu 18.04, follow the instructions in the “Installing Using a PPA” section of How To Install Node.js on Ubuntu 18.04.
The Yarn package manager installed on your local machine or development server. You can following the installation instructions in the official documentation.
Ruby, rbenv, and Rails installed on your local machine or development server, following Steps 1-4 in How To Install Ruby on Rails with rbenv on Ubuntu 18.04. This tutorial uses Ruby 2.5.1, rbenv 1.1.2, and Rails 5.2.3.
SQLite installed, following Step 1 of How To Build a Ruby on Rails Application. This tutorial uses SQLite 3 3.22.0.
Redis installed, following Steps 1-3 of How To Install and Secure Redis on Ubuntu 18.04. This tutorial uses Redis 4.0.9.
