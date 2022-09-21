# Fantasy Tutorial

This section includes the tutorial we wish we could write for the
OCaml tools.  Still very much in development.

## The ideal experience

The ideal setup experience is to... have no steps at all.
This is possible recently by using [devcontainers](https://containers.dev),
which is a metadata standard that allows IDEs and cloud services
like GitHub CodeSpaces to launch a development environment.

The Real World OCaml v2 includes sufficient metadata to make this
just work.  You can clone the book repository and open it in VSCode,
and it will automatically configure a container with the right tools
in place. Similarly, you can open the repository in GitHub Codespaces
and it spins up a tutorial.

While this is a great first user experience, there is still some
work to be done for a truely native tools install.  A tutorial should
subsequently cover the next step for a native installation after
the user has gotten started using development containers.

## Preliminaries

Before starting the tutorial proper, what are the steps we want the
tutorial to cover?

### Setup/initializaion

- Should cover common use-cases
- Maybe: Linux (e.g., on a VM), Mac, locally, and Windows, via WSL2.
- Install basic tools
- We could "cheat" and do it via containers, i.e., get them to install
  Docker first.
  - But the container is hiding complexity of the underlying tools in
    a way that's going to come out when someone needs to write their
    own docker setup, or to do a local install. So there's a real
    tradeoff here.
