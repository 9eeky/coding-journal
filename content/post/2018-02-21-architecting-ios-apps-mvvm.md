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