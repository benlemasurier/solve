# Solve
[![Gem Version](http://img.shields.io/gem/v/solve.svg)][gem]
[![Build Status](http://img.shields.io/travis/berkshelf/solve.svg)][travis]

[gem]: https://rubygems.org/gems/solve
[travis]: http://travis-ci.org/berkshelf/solve

A Ruby versioning constraint solver implementing [Semantic Versioning 2.0.0](http://semver.org).

## Installation

    $ gem install solve

## Usage

Create a new graph

    graph = Graph.new

Add an artifact to the graph

    graph.artifact("nginx", "1.0.0")

Now add another artifact that has a dependency

    graph.artifact("mysql", "1.2.4-alpha.1").depends("openssl", "~> 1.0.0")

Dependencies can be chained, too

    graph.artifact("ntp", "1.0.0").depends("build-essential").depends("yum")

And now solve the graph with some demands

    Solve.it!(graph, ['nginx', '>= 0.100.0'])

Or, if you want a topologically sorted solution
NOTE: This will raise Solve::Errors::UnsortableSolutionError if the solution contains a cycle (which can happen with ruby packages)

    Solve.it!(graph, ['nginx', '>= 0.100.0'], sorted: true)

## Authors

* [Jamie Winsor](https://github.com/reset) (<jamie@vialstudios.com>)
* [Andrew Garson](andrewGarson) (<agarson@riotgames.com>)
* [Thibaud Guillaume-Gentil](https://github.com/thibaudgg) ([@thibaudgg](http://twitter.com/thibaudgg))
