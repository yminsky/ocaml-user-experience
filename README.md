---
title: A vision for the OCaml user-experience
---

The goal of this document is to sketch out goals for what the OCaml
user-experience should look like.  This is less about any particular
tool or technology, and more about what it should feel like to users.

# Objectives

## The experience for newbies is simple

Part of this is that users should not be exposed to many different
control services.  Users should have a single tool through which the
majority of their interactions happen.

Also, the experience for setting up a new project and starting to
write code should have as few steps as possible.

## The workflow for newbies scales up seamlessly to larger projects

Note that "seamlessly" doesn't mean "without change".  Large, complex
projects have different needs than simple ones, and developers of
complex projects should have the ability to take on more complexity in
their setup.

But that extra complexity should come incrementally, and their
shouldn't be a need to completely shift tools or approaches as a
project grows and evolves.

## The tools are opinionated and have good defaults

Part of the way that we make the newbie experience simple is by making
choices by default.  These opinions should extend to tools (e.g., set
up ocamlformat by default), but not to libraries (the system shouldn't
pick an HTTP library for you.)

## The tools can and do evolve, but without routinely breaking existing projects and tools

This is something that Dune does a good job on for the most part
already.  In particular, Dune supports multiple historical versions,
so the addition of a new version with new behavior doesn't break old
projects.

This should be true pervasively for the core tools.

## The out-of-the-box experience is complete

When you set up a new project in the standard way, you should have all
of the foundational tooling up and working, with a minimum of fuss.
This includes:

- Autoformatting (ocamlformat)
- Type-throwback, highlighting type errors, go-to-definition,
  autocompletion (merlin)
- Doc generation (odoc)
- Workflows for kicking off builds and tests, and automation for
  walking through compiler errors.

It's worth noting that the degree to which this is possible will
depend on editors, and so the best version of this workflow should
work most smoothly with the most popular editor choice (i.e., vscode),
with more setup being acceptable for other editors.

That said, the command-line experience must still be efficient and
convenient.