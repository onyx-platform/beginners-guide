# Chapter 2: The Keys to Dynamic Analytics

Let's take some time now to explore what it good dynamic analytics systems. We're going to dive into the problems with current approaches and start to sketch out an alternate solution. I get asked a lot "Why *did* you build Onyx anyway?" I hope this chapter justifies its extistence, and demonstrates how radically difference Onyx's approach is to distributed computation.

## The fundamental problem

I'll assert that to build good analytics applications, the foundation trait that your design needs it to *pull apart* the different pieces of the computation. Modern platforms frequently give you one level of abstraction to work with: collections processing. It's certainly alluring abstraction. What could be more comfortable than working with something that *feels* like function composition, but can be transparently applied to petabytes worth of data?

Collections processing (Spark), pipe assembly (Cascading), and SQL descriptions (Hive) all suffer from the same trait - they conflate the computational structure, execution context, resource lifecycles - to name but attributes. Exposing an API of *only* code is poison to the developer who's trying to make truely dynamic systems. Dynamic systems, by their very nature, know little-to-no information about their programmatic execution at compile time. Such systems must communicate in a machine-to-machine fashion, assembling their computations at runtime. These communication lines need to cross programming languages, networks, and time. A code-only API doesn't help us much.

Let's be a bit more concrete:

```clojure
(defn f [x]
  (inc x))

(defn g [x]
  (* x 2))
```

Here we have two simple functions, `f` and `g`. What can we learn about `f` and `g` at runtime?

```text
user=> f
#<user$f user$f@4e573858>

user=> g
#<user$g user$g@709dd654>
```

Hmm, that's not very helpful. At least we can see the function name in the output. Distributed processing is all about building up computations, so let's take it further:

```clojure
(def h (comp f g))
```

`h` is the composition of `f` and `g`. What can we learn about `h` at runtime?

```text
user=> h
#<core$comp$fn__4192 clojure.core$comp$fn__4192@271796d3>
```

That's not terribly helpful. To be clear, I'm *not* criticizing Clojure here. The point that I'm making is that composition of code obscures the structure of what lies within the computation. Make no mistake: **an inability to understand the structure of your distributed processing program at runtime is deadly for diagnosing problems**.

How can we work around this problem? As Clojurists, we know the that if we're not working with code, then we're working with data. Strong analytics systems are aggressively data drive. Data interfaces make your designs simpler, and that increases business opportunity. The technique that we need to employ is similar to how Clojure treats side effects. We don't pretend that code is absent from our programs. Rather, we *minimize* the use of code and describe our programs as data as the norm.

There are lots of great papers and talks out there on why data driven systems are often superior - I'd recommend searching around. I'm going to spend the rest of this chapter calling out the advantages that are gained specifically for distributed data processing systems.

## Sharing immutable values across tenants

One of the main principles of being able to share values is it avoids many problems with concurrency. There's no harm in sharing a value if no one is going to mutate it. An extensions of this property is that you can share values across *tenants*. Analytics systems are often multi-tenanted. That means that there are disparate sections of data for different consumers, and consumers shouldn't see each one another's data.

On the other hand, to the extent that the *descriptions* of your computations are data, you become free to share these across tenants. Computations across tenants are often similiar in structure, flow, and transformation type. You can imagine building up a catalog of values that enumerate all possible elements of a computation that your system offers, and sharing that catalog across tenants in your system.

## Debugging live values

If you're going to build a reliable system, you need to be able to understand how it's behaving when it's live. As more of your computational description becomes data, the easier it becomes understand what the computation is at runtime. One critical trait of Clojure's data structures are that they print to human-readable formats. This is decisive in understanding what instructions each node in your cluster has received while it's live in production.


