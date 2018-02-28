# Chapter 1: Introduction

This is the very beginning of the official guide to learning Onyx. You're probably here because you heard about Onyx, and you sort of know what it is, but the picture is still fuzzy. That's okay! Learning to use a distributed system is an inherently difficult task. There are, by definition, a lot of moving parts. The abstractions are usually foreign, you're dealing with multiple machines, and there's likely a big chunk of data that you're trying to work with! I can sympathize. I'm going to take you through a journey of how to use Onyx effectively. By the end, I hope you're as excited as I am to start building applications with Onyx!

## About this guide

There're a lot of things that I'm going to touch on in this guide, so feel free to read it straight through, or skip around. It's split up into 10 chapters. The first 3 chapters cover distributed data processing as a general topic. Before we dig into how to use Onyx, I want to establish the principles that I believe good data processing software is built ontop of. Grab a coffee, pour a glass of wine - whatever suits you. Sit back and have a gentle read about the approach we're taking. With that behind you, you'll have a more intuitive understanding about how things work when we start fiddling with Onyx's API.

Chapter's 4 and 5 delve into Onyx itself. Chapter 4 introduces the basic constructs that you'll be working with to interact with the API. Hopefully you'll make the connection between the concepts from the previous chapters and their manifestion in Onyx. Chapter 5 gives you *just enough* information about the architecture of Onyx to make intelligent decisions. I could go on for pages and pages about the architecture, but once you have the basic idea down, you'll be able to reason about the behavior of your cluster without too many problems.

In Chapter 6, we get hands on. We'll develop a sample application with Onyx and build on it by progressively adding challenges to the problem. I always found that I learned these types of platforms best when I was able to get hands on with a slow, carefully guided example. Along the way, we'll break things and develop an understanding of how to diagnose errors. We'll work locally so that you don't have to set up any external cloud provider services. If you want to deploy to the cloud, keep reading!

Chapters 7, 8, and 9 cover things you ought to know if you're going to put Onyx into production. We'll talk about how you might want to go about standing up your basic cluster infrastructure, options for deployment, and monitoring what Onyx is doing when it's live.

We'll close out the guide with Chapter 10 - extending Onyx. We like to say that Onyx is "Ad-hoc anything" - it feels almost infinitely flexible. I'll point you to the extensions features that Onyx exposes and give you a taste of how you can bend Onyx to your will.

## What is Onyx anyway?

To be precise, the platform that you're about to pick up is a masterless, fault tolerant, distributed data processing system. If these are new terms to you, the next chapter will help you get grounded with this topic. Let's put it in simpler terms. (Data processing) Onyx is a platform that allows you to read large amounts of data and perform transformations on that data. (Distributed) When your data set gets large enough, you can add more machines to compute answers faster. (Fault tolerant) If a machine in your cluster fails, Onyx can recover transparently. (Masterless) Onyx's architecture is exceptionally unique in that there is no single coordinating process orchestrating the rest of the cluster.

I like to use "data processing" and "analytics" interchangeably. This isn't always correct, but for me, it captures the essence of what we're doing. Typically, the reason that we're building a data processing application is to *answer questions*. It's rare that single data points are of interest. More often, we want to take a summation, find absolute upper and lower bounds, and roll up data across tenants. We're *analyzing* what's going on with the data set.

Onyx is a platform that helps you answer questions as flexibly as possible. Every piece of Onyx has been built with dynamism in mind. To that end, I hope you enjoy the symbiotic nature between Onyx and Clojure itself.

## What you'll need

To work through this guide, you're going to need Java 8, Git, and [Leiningen](http://leiningen.org) installed. I'll presume you can take care of that.

## Who am I?

My name is [Michael Drogalis](https://twitter.com/MichaelDrogalis), and I'm the creator of this beast!
