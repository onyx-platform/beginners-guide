# Chapter 4: The Elements of Onyx

Now that we've had a discussion about the core problems with collections-processing oriented frameworks, we're going to take the alternative ideas that we discussed and give them some character. We're going to walk through a series of *constructs* that are a direct result of taking a purposefully data oriented approach. These constructs are what you use to build Onyx programs.

## The big idea

The central idea behind the interface that Onyx exposes to you is that you need not learn any new abstractions. Instead, we reuse the abstractions that we use all the time - data structures and functions. Using these two concepts allows us to move fluidily throughout the stack, avoiding impedence mismatch problems that slow engineering effort down. The rest of this chapter will reflect the division of all components into either of these categories.

## Segment

A segment is the smallest unit of data in Onyx, and it's represented by a Clojure map. As data moves between machines on your cluster, data is always sent and received as a map.

## Function

Onyx uses plain Clojure functions to carry out distributed data transformation. These functions take a segment as a parameter and outputs either a segment or a sequence of segments. Functions are meant to literally transform a single unit of data in a functional manner. You can parameterize these functions if you need to, and we'll demonstrate how to do this in the example application.

## Workflow

A workflow is the structural specification of an Onyx program. Its purpose is to articulate the paths that data flows through the cluster at runtime. It is specified via a directed, acyclic graph. This is what we mean when we say that we're *capturing the structure* of an analytics program.

## Catalog



