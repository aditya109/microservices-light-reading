# Table of Contents

- [What Makes a Good Service?](#what-makes-a-good-service-)
  * [Loose Coupling](#loose-coupling)
  * [High Cohesion](#high-cohesion)
- [The Bounded Context](#the-bounded-context)
  * [Shared and Hidden Models](#shared-and-hidden-models)
  * [Modules and Services](#modules-and-services)
  * [Premature Decomposition](#premature-decomposition)
- [Business Capabilities](#business-capabilities)
- [Turtles All the Way Down](#turtles-all-the-way-down)
- [Communication in terms of Business Concepts](#communication-in-terms-of-business-concepts)
- [The Technical Boundary](#the-technical-boundary)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

# What Makes a Good Service?

## Loose Coupling

When services are loosely coupled, a change to one service should not require a change to another.

A loosely coupled service knows as little as it needs to about the services with which it collaborates.

This also means we probably want to **limit the number of different types of calls from one service to another**, because the potential performance problem, *chatty communication can lead to tight coupling*.

## High Cohesion

We want related behavior to sit together, and unrelated behavior to sit everywhere.

**Making changes in lots of different places is slower**, and **deploying lots of services at once is risky** - both of which we want to avoid.

So we want to find boundaries within our problem domain that help ensure that related behavior is in one place, and that communicate with other boundaries as loosely as possible.

# The Bounded Context

The idea is that any given domain consists of multiple bounded contexts, and residing within each are *things that do not need to be communicated outside* as well as *things that are shared externally with other bounded contexts*. Each bounded context has an explicit interface, where it decides what models to share with other contexts.

OR,

A specific responsibility enforced by explicit boundaries. If you want information from a bounded context, or want to make requests of functionality within a bounded context, you communicate with its explicit boundary using models.

> *Cells can exist because their membranes define what is in and out and determine what can pass.* 

## Shared and Hidden Models



## Modules and Services

## Premature Decomposition

# Business Capabilities

# Turtles All the Way Down

# Communication in terms of Business Concepts

# The Technical Boundary