# Chapter 4: The Elements of Onyx

Now that we've had a discussion about the core problems with collections-processing oriented frameworks, we're going to take the alternative ideas that we discussed and give them some character. We're going to walk through a series of *constructs* that are a direct result of taking a purposefully data oriented approach. These constructs are what you use to build Onyx programs.

## The big idea

The central idea behind the interface that Onyx exposes to you is that you need not learn any new abstractions. Instead, we reuse the abstractions that we use all the time - data structures and functions. Using these two concepts allows us to move fluidily throughout the stack, avoiding impedence mismatch problems that slow engineering effort down. The rest of this chapter will reflect the division of all components into either of these categories.

## Segment

A segment is the smallest unit of data in Onyx, and it's represented by a Clojure map. As data moves between machines on your cluster, data is always sent and received as a map.

Example:

```clojure
{:user-id 42}
```

## Function

Onyx uses plain Clojure functions to carry out distributed data transformation. These functions take a segment as a parameter and outputs either a segment or a sequence of segments. Functions are meant to literally transform a single unit of data in a functional manner. You can parameterize these functions if you need to, and we'll demonstrate how to do this in the example application.

Example:

```clojure
(defn my-function [segment]
  (update-in segment [:user-id] inc))
```

## Workflow

A workflow is the structural specification of an Onyx program. Its purpose is to articulate the paths that data flows through the cluster at runtime. It is specified via a directed, acyclic graph. This is what we mean when we say that we're *capturing the structure* of an analytics program.

Example:

```clojure
[[:input-task :increment-task]
 [:increment-task :output-task]]
```

## Catalog

A catalog is a listing of all possible elements, or *tasks*, that can appear in your workflow. Catalogs are the place where you parameterize the tasks that you'll submit as your job.

Example:

```clojure
[{:onyx/name :in
  :onyx/ident :core.async/read-from-chan
  :onyx/type :input
  :onyx/medium :core.async
  :onyx/batch-size batch-size
  :onyx/max-peers 1
  :onyx/doc "Reads segments from a core.async channel"}

 {:onyx/name :inc
  :onyx/fn :onyx.peer.min-peers-test/my-inc
  :onyx/type :function
  :onyx/batch-size batch-size}

 {:onyx/name :out
  :onyx/ident :core.async/write-to-chan
  :onyx/type :output
  :onyx/medium :core.async
  :onyx/batch-size batch-size
  :onyx/max-peers 1
  :onyx/doc "Writes segments to a core.async channel"}]
```

## Flow Conditions

Flow conditions specify on a segment-by-segment basis which direction data should flow determined by predicate functions. This is helpful for conditionally processing a segment based off of its content.

Example:

```clojure
[{:flow/from :input-stream
  :flow/to [:process-adults]
  :flow/predicate :my.ns/adult?
  :flow/doc "Emits segment if this segment is an adult."}]
```

## Lifecycles

Lifecycles are a feature that allow you to control code that executes at particular points during task execution on each peer. Lifecycles are data driven and composable.

Example:

```clojure
[{:lifecycle/task :my-task-name-here
  :lifecycle/calls :my.ns/calls
  :lifecycle/doc "Test lifecycles and print a message at each stage"}]
```

