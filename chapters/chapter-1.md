# Chapter 1: Introduction

This is the very beginning of the official guide to learning Onyx. You're probably here because you heard about Onyx, and you sort of know what it is, but the picture is still fuzzy. That's okay! Learning to use a distributed system is an inherently difficult task. There are, by definition, a lot of moving parts. The abstractions are usually foreign, you're dealing with multiple machines, and there's likely a big chunk of data that you're trying to work with! I can sympathize. I'm going to take you through a thorough journey of how to use Onyx effectively. By the end, I hope you're as excited as I am to start building applications with Onyx!

## About this guide

There's a lot of things that I'm going to touch on in this guide. It's split up into 11 chapters. The first 4 chapters cover distributed data processing in the general sense. Before we can dig into how to use Onyx, I want to establish the principles that I believe good data processing software is built ontop of. Grab a coffee, pour a glass of wine - whatever suits you. Sit back and have a gentle read about the approach we're taking. With that behind you, you'll have a more intuitive understanding about how things work when we get into Onyx's API.

Chapter's 5 and 6 delve into Onyx itself. Chapter 5 introduces the basic constructs that you'll be working with to interact with the API. Hopefully you'll make the connection between the concepts from the previous chapters, and their manifestion in Onyx. Chapter 6 gives you *just enough* information about the architecture of Onyx to make intelligent decisions. I could go on for pages and pages about the architecture, but once you have the basic idea down, you'll be able to reason about the behavior of your cluster without too many problems.

In Chapter 7, we get hands on. We'll develop a sample application with Onyx and build on it by progressively adding challenges to the problem. We'll work locally so that you don't have to set up any external cloud provider services. If you want to deploy to the cloud, keep reading!

Chapters 8, 9, and 10 cover things you ought'a know if you're going to put Onyx into a production environment. We'll talk about how you might want to go about standing up your basic cluster infrastructure, options for deployment, and monitoring what Onyx is doing when it's live.

We'll close out the guide with Chapter 11 - extending Onyx. We like to say that Onyx is "Ad-hoc anything" - it feels almost infinitely flexible. I'll point you to the extensions features that Onyx exposes, and give you a taste of how you can bend Onyx to your will.

## What you'll need

To work through this guide, you're going to need Java 8, Git, and [Leiningen](http://leiningen.org) installed. I'll presume you can take care of that.

## Who am I?

My name is [Michael Drogalis](https://twitter.com/MichaelDrogalis), and I'm the creator of this beast!