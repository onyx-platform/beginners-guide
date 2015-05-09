# Chapter 2: Distributed Systems Basics

So you want to learn a distributed system? If this is your *first* distributed system, you'll find that this world is substantially more complicated than that of a single machine. Namely, so many more things go wrong! Machines can go down, networks can partition, garbage collectors can stop the world - the number of failure scenarios is endless. The first thing to do is start considering failure as the *norm*. As the number of nodes that you work with increases, the chances of any single node in your cluster having a problem increases. So where does that leave us?

## It's tough to build

The process of *building* something like Onyx is tricky. Onyx has to cope with all the failures that I outlined above. Moreover, it has to do it relability. The last thing we want is for end users to be questioning whether Onyx really does what we say it does! I mention this because, at some level, you need to be aware of the types of failures that can occur. In order to intelligently design your application, you need to know how Onyx is going to behave when trouble arises. This is a fundamental skill to architecting solid systems.

## It's tough to learn

Earlier I mentioned that learning these types of software packages are hard - not a very flattering thing for me to say! Well, it's true! There're a lot of concepts that come along with working with a distributed data processor. Most of these concepts are a direct result of the inate complexity in dealing with the physics of your program being spread out over multiple machines. But - this *doesn't* mean that all the concepts that we use in distributed data processors need to be new. A basic value proposition of Onyx is that the abstractions we expose are the same ones we use all the time in single node functional programming - data structures and functions.

## Computing the world

What exactly *is* Onyx? Onyx is a distributed data processor. In its most basic terms, that means that you can write a program that transforms and aggregates data. Your program is built against a special interface. Onyx understands this interface, and can automatically work with your program on multiple machines in a cluster. By clustering your program, Onyx can give it *more data*. The more machines you give Onyx, the faster it can go. And in fact, Onyx's performance gains are predictable and linear. If you're 3 node cluster is processing 3 million messages per second, adding *another* 3 machines will bring your total throughput to 6 million messages per second.

Alright, we have multiple machines and lots of data? Is there anything else we should know? Absolutely! There are two main types of distributed computation - batch and streaming. I'll talk about both, but I want to briefly mention that Onyx is a *hybrid* - meaning it can handle both batch and streaming workloads. Most platforms of this nature strictly operate on one or the othere. There are huge advantages to being able to transparently switch between these, but we'll get into that later!

### Batch computation

### Stream processing

## The competition

