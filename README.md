# Developer Portal

## Purpose

This repository allows to build the developer portal hosted at: [https://developers.windingtree.com](https://developers.windingtree.com).


## Dependencies

* [Ruby](https://www.ruby-lang.org/)
* [Jekyll](https://jekyllrb.com/)
* [Bundler](https://rubygems.org/gems/bundler)

```shell
gem install jekyll bundler
```

## Local Development

Clone the repository

```shell
git clone https://github.com/windingtree/developer-portal.git
```

Change to the repository's directory:

```shell
cd developer-portal
```
Install the gem dependencies:

```shell
bundle install
```

Build and launch the server

```shell
bundle exec jekyll serve
```

Browse to [http://localhost:4000](http://localhost:4000)

## Creating Diagrams

[PlantUML](https://plantuml.com/) diagrams can be added thanks to the `https://github.com/Patouche/jekyll-remote-plantuml` plugin.

  {% uml %}
  Bob -> Alice : Hello 
  {% enduml %}