Some concrete ideas about how the core OCaml workflow should work.

## Dune (and the editor) as the primary front-end

By and large, users should have only one command-line tool they
interact with on a regular basis, and on the command-line, that tool
should be dune.

For users who prefer an IDE-style experience, like that available in
vscode and in emacs if it is configured for it, the editor itself
should be the primary interface.  The command-line should be
convenient and intuitive to use alongside the editor, but users should
rarely or never need to reach for the command-line.

## Dune as the build orchestrator

Right now, we have two tools that orchestrate builds: opam and dune.
They do this in different ways: opam isn't a full build system,
instead invoking the build system chosen for each package, whereas
dune takes full control over the build.

We should unify these two different bits of functionality.  Package
authors can still use whatever build system they want, but they must
integrate with dune, as a foreign build.

The process of creating a foreign build should be smooth: simple to
set up, and well documented.  But functionality should be added only
for dune users when that will make it materially easier to make
progress and improve the developer experience.

We shouldn't describe this as a "monorepo" workflow.  A true monorepo
workflow is where you commit the code of all packages you're using
into the directory where you're building.  But that's not a choice we
should enforce, since it has serious downsides (repo bloat, difficulty
of code review). Really, this is more like a standard lockfile style
workflow.

## Dune as the cache

In this world, developers will have multiple directories set up for
using OCaml, many of them sharing the same version of OCaml and the
same version of multiple libraries.

Dune's caching and sharing mechanisms should be the way this should be
optimized, rather than the current world where dune and opam each have
their own caching mechanisms.

## Keep the command-line minimal

There are two reasons for this:

- Command lines are harder to version, and a minimal command-line is
  less likely to break.
- It's good to have a single source of truth for configuration.
  Command-line tools become another place to state configuration, and
  in the end that configuration ends up in shell scripts and the like,
  which makes the configuration harder to find.

## Configs in files

This is the dual to the previous point: if you don't specify
configuration on the command line, it has to go somewhere.  That place
should be in config files in the directory that you've set up for
OCaml use.

## Editing configs

## No ambient install

Today, opam by default installs OCaml along with a set of libraries
and tools that are in your PATH by default, and you can mutate that
default by changing your switch.

This workflow should go away entirely (except when you directly invoke
the now deprecated opam command-line tool, and that should eventually
simply be retired.)  You can only set up OCaml within a directory.

## Watch-mode as the default

The user experience should default to using watch-mode, and having
good ways for users to see errors when they come up.  This is
important because it provides a fast form of feedback when editing
configs.

## Batch interaction is first class

Despite watch-mode being the default experience, batch interaction,
where you directly instruct the building of a given item, should be
first class, and should work in a predictable way.  This is important
because batch interaction needs to work well when scripting a build.
Also, it's an approach that some power users will strongly prefer.

## Configs should be discoverable and easy to edit

Editing of configs should be really simple for users. This suggests a
few things:

- There should be excellent documentation for configs and config
  options.
- Common changes to config files should be lightweight and idiomatic
  to the users interaction environment.  But that means different
  things for vscode and for vim users.

*Open question:* should we support git-style command-line tools for
updating configs?  This is in tension with the goal of keeping the
command-line minimal.

Also, it's important that there be a simple and minimal set of config
files, and it should be clear when you have to use one file or
another.  And users shouldn't have to edit config files in multiple
different formats.

This suggests that there should be no free-standing opam config
files, but this may be impractical for compatibility and transition
reasons.  A reasonable alternative is to have opam config files be
auto-generated, so they never need to be edited by users.  Another
approach would be for opam files to be usable as a transitional
matter, but to not be required in cases where configs are fully
contained in Dune.
