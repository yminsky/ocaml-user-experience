# Objectives for the OCaml Developer Experience

The goal of this document is to sketch out goals for what the OCaml
developer-experience should look like.  This is less about any
particular tool or technology, and more about what it should feel like
to developers.

The objectives themselves are phrased as statements that we want to be
true, rather than things that have already been achieved.

## It's easy for newbies to get started

Part of this is that users should not be exposed to many different
control services.  Users should have a single tool through which the
majority of their interactions happen.

Also, the experience for setting up a new project and starting to
write code should have as few steps as possible.

When there's a choice between keeping the newbie experience simple and
conveniently supporting advanced workflows, we should prefer a simple
newbie experience, though we should be more reluctant to make a
sensible advanced workflow practically impossible.

## Workflows are built around a coherent, understandable model

It's not enough for it to be easy to get started.  The development
model should also have a simple model that developers can reason
about.  When possible, we should remove complexity, rather than cover
it over with convenient tools.

While supporting legacy users is important, we should deprecate and
eventually abandon workflows that detract from having a simple core.

## The workflow for newbies scales up seamlessly to larger projects

Note that "seamlessly" doesn't mean "without change".  Large, complex
projects have different needs than simple ones, and developers of
complex projects should have the ability to take on more complexity in
their setup.

But that extra complexity should come incrementally, and their
shouldn't be a need to completely shift tools or approaches as a
project grows and evolves.

Similarly, it should be as easy for new users to get started with building
a large OCaml project as it is for a simple one.

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

## The tools are helpful, especially to newbies

The tools should go out of their way to make it easy for people who
are encountering some aspect of the tool for the first time.

For example:

- Tools should provide helpful feedback for users when they make
  common mistakes, like misspelling a subcommand, or trying to start a
  build before creating the necessary build files.

- Tools should prefer helpfulness over concision. Better to spend a
  few extra words to suggest a likely solution, than to concisely say
  what exact problems was found, but without helping the user towards
  a solution.

## Sharing code and docs should be straightforward

There should be little gap between developing OCaml code, and getting
the project into a form where it can be published.  Ideally, errors
that make a project unsuitable for publication on opam (e.g. metadata
or dependency errors) should be caught during the normal development
workflows and not upon submission to a central package repository.
