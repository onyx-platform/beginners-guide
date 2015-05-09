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

## Automatic database schema generation

A distinct trait of highly flexible, dynamic analytics applications is their ability to store computations to be run at different points in time. Code descriptions of computations are terribly complex to serialize to a database. We'd prefer to skip this mess altogether and serialize *data* to a database. If you use a platform that communicates data via its interfaces, you can work this to your advantage and automatically generate database schemas. Your data driven computation descriptions will serialize neatly to a database without any human intervention.

## Automatic user interface generation

By the same token as database schema generation, user interfaces can also be generated. A large component of the effort in building analytics systems is constructing the user interfaces that humans create computations with. Using immutable values that can cross the wire without modification to ClojureScript saves massive amounts of time on this front. The trick is having a backend platform that communicates through its interfaces with those *same* data structures.

## Generative testing

Clojure has a strong heritage in employing many different types of testing - not the least of which is generative (or property-based) testing. When the bulk of your computation description is data, you can intelligently mix and match pieces of these descriptions and generatively test hundreds of millions of test cases without breaking a sweat.

## Runtime variable substitution

Many computational descriptions need to be *parameterized*. You'll often need to feed in a database connection URL, a port number, or a secret access key. When you're working primarily with code, it's too easy to let these variables get stuck inside your functions. Your programs become far cleaner and more expressive when runtime variable substitution is an explicit feature that you can work with.
