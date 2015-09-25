# Powa GitHub Site

The [powa.github.io](http://powa.github.io) site for open source and documentation.

## Getting Started

### Ruby

We recommend using a Ruby management tool like [rvm](http://rvm.io) or [rbenv](https://github.com/sstephenson/rbenv) or [pik](https://github.com/vertiginous/pik) to manage Ruby and Gems.

### Bundler

Install [bundler]() if you don't already have it (you might need sudo):

    $ gem install bundler

### Gem installation

Install the dependencies:

    $ bundle install

## Running Locally

Deploy the site locally by running the serve command in the root of the project:

    $ bundle exec jekyll serve --watch

Just refresh the page to pick up most changes -- config / yaml changes require a server restart.

## Development

Create feature branches off of the `develop` branch:

    $ git checkout develop
    $ git checkout -b feature/feature_name

Issue a pull request when you are ready for review.  If approved your changes will be staged for the next deploy.

## GitHub Page Management

You need to be a part of the Powa Github organization and have access rights to `https://github.com/powa/powa.github.io.git` in order to publish to the [GitHub site](http://powa.github.io).

### Setup

Add the Github remote:

    $ git remote add github git@github.com:powa/powa.github.io.git


Merge changes to the `master` branch and push to the `powa.github.io` repository:

    $ git push github master
