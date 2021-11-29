---
title: "MVC vs MVT (React and Django)"
date: "2021-11-28T07:26:03.284Z"
description: "A short blurb on MVC, MVT, MVVM, with React and Django examples."
categories: [software architecture, React, Django, MVC, MVT, MVVM]
comments: true
---

As someone who develops with React on a day to day basis, the **M**odel **V**iew **C**ontroller (MVC) is a architectural paradigm that I _should_ know more about, but I don't.

I've read about in in React documentation when I was just starting out with it, have heard it mentioned in interviews, and now have heard about its counterpart - the **M**odel **V**iew **T**emplate - while trying to pick up Django.

It's about time for me to hash out what each of these mean and gain a solid understanding of each.

So what do each of these excel at, what types of problems do they solve, and where can I commonly find each of these?

This little code bite seeks to answer these questions.

## Model View Controller (MVC)

The MVC framework separates the code into three components, with a unidirectional data flow:

1. Model - The layer deals with data-related logic. It retrieves, changes, and saves data to the database.
2. View - The presentation layer responsible for collecting data from the model or user and presenting it. Everything in the browser GUI falls under view
3. Controller - This layer controls the data flow and interaction between the view and model layer.

Pros:

1. makes it easy to develop large applications
2. easy for multiple developers to collaborate and work together

Disadvantages:

1. view is controlled by model and controller
2. not suitable for small applications

## Model View Template (MVT)

The MVT (or MTV) framework also separates code into three parts:

1. Model - This layer contains code responsible for dealing with data and databases.
2. View - This layer decides what data should be displayed, rather than like the Controller does in the MVC framework.
3. Template - This layer specifies a structure for an output.

Pros:

1. Less coupled
2. suitable for small to large scale applications
3. easy to modify

Disadvantages

1. sometimes confusing to understand the flow
2. modification of models/views should be done carefully without affecting templates

The main difference between MVC and MVT is that a MVC has their controller determine what should be shown, but in a MVT we already have a template, and the framework (via the View layer) helps determine the controller part itself.

So, for a MVC pattern, we manage the state of the application and have the view controlled by the controller and the model.

In an MVT, the view itself queries the model and processes the results from the model. The view fills in a template and sends it to a user. Here, the view is not coupled with a model, and thus becomes more loosely coupled and more easy to modify than a MVC.

## React

Often times people think about React and MVC together. React, though easy to implement the MVC framework with, is in it of itself not an MVC framework. React is just a _library_ for building composable user interfaces. React was introduced as a new option that stemmed away from traditional web application UIs that were built using templates or HTML directives (like Django did).

### Model View View-Model (MVVM)

It's been said that your React project can take on the form of a more MVVM design, where the [View-Model is the component related code that manages simple state, passes data directly onto View, and potentially passes data directly back from View.](https://stackoverflow.com/questions/51506440/mvvm-architectural-pattern-for-a-reactjs-application) It is argued that MVVM is a more accurate depiction of most React applications (excluding when you implement [Flux React](https://facebook.github.io/flux/) and as a result enforces unidirectional data flow) as MVVM includes bidirectional data flow - something most React applications have.

## Django

Django began as a web _framework_ that allows users to follow along the MVT design principle (but with the right configuration, can also move away from that). Django is usable for both the front and backend and comes along with a lot of extra bells and whistles. For me, that's something to dive deeper into!

You might find Django labeled as a MVC pattern, as it "follows the pattern closely enough to be called one." I agree since I kind of have to fold some ideas to fit into the MVC pattern a bit, but for me Django seems better suited with the MVT/MTV framework due to Django's use of templates. There's a slight distinction that is [better hashed out here.](https://djangobook.com/mdj2-django-structure/)

## In summary

For me, after this little bit of research, I've found that React follows more of a MVVM framework due to its bidirectional data flow, unless you implement Flux React, which then more closely follows the MVC framework due to its unidirectional data flow. Django follows the MVT/MTV design more closely, but has been confused with the MVC design principle in the past. The MVC has the controller and acts as a coordinator between the View and the Model, and apparently [ASP.NET](http://ASP.NET) uses the MVC design.

React is just a UI library component that is not very opinionated, and allows for you to play into various types of architecture as your web application needs. Django is a web development framework that is super strong (as in, it has a lot of easy to add functionalities) and encompasses both backend and frontend.

When using React, it may be confusing to decide on which architectural design principle to use. For me, I'll probably stick to the MVVM format and focus on designing components that are loosely coupled and modular - all the general good coding design principle jazz. I enjoy using React a lot, and don't see myself using Templates any time soon (with Django). I'll try my hand at using Django just for developing RESTful APIs.
