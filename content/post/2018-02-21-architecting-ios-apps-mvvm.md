+++
Categories = ["Swift", "iOS"]
Description = ""
Tags = ["Swift", "iOS"]
author = "Igor Kulman"
date = "2018-02-24T09:29:12+01:00"
title = "Architecting iOS apps: MVVM"
url = "/architecting-ios-apps-mvvm"

+++

When switching from Windows Phone development to iOS I had about 3 months to learn iOS and Swift before starting the work on an actual iOS application. I had a chance to build the application from scratch with a colleague so I wanted the application to be really well written and architected. 

I started to look at some iOS tutorials and other peoples' iOS code. There were three big things in particular that I disliked, that I want to show you together with solutions I found. This second post deals with **separating the application logic from its presentation**. 

* [Part 1: Coordinators](/architecting-ios-apps-coordinators)
* Part 2: MVVM (this post)

<!--more-->

### The problem

When going through some iOS tutorials I found code like this a lot in view controllers

<div data-gist="189dc6afea62f6418793d862ab63d8d6" data-file="badcode.swift"></div>

I have a problem with code like this. In my opinion the view controller should not handle stuff like database or API calls. It should be just concerned with presenting the UI and handling user interaction, nothing more. Most iOS applications put all the logic for everything into the view controller making MVC the Massive View Controller pattern. 

In the [previous post about coordinators](/architecting-ios-apps-coordinators) we moved the navigation logic from the view controller into a coordinator, in this post we will continue making the view controller thinner by separating the application logic. Basically we need to add a layer between the UI (or view, represented by the view controller) and the model (represented by the database, API, etc. ). If only there was a pattern for that ...

### The solution: MVVM

The solution is the Model View ViewModel pattern, or MVVM for short. This pattern originated in the Microsoft world that I come from and has been around for many years. You can find many explanations online, some better than others. Lets try to explain in in the context of iOS.

Lets image the ViewController as a **View**. It is responsible for showing the user the UI of the app on the screen and interacting with the user in form of reacting to the input from the user. This is all the View is supposed to do, nothing else. 

The **Model** is basically the same as what you would call a Model in the iOS world; some database, some remote API, etc. 

MVVM introduces a new layer called the **ViewModel**. The ViewModel is a layer that sits between the View and the Model. It reads data from the Model (e.g making API calls) and updates the Model (e.g saving data to the database). It know nothing about what the UI looks like or how the user interacts with the application. On the other hand it exposes some data and methods to the View. The View uses that data to display it in the UI and calls those methods in response to some actions invoked by the user in the UI. 