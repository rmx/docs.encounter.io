# docs.encounter.io

This is the documentation for `encounter.io`. It's built with [nanoc][nanoc].

## Instructions

To build the site locally:

    <setup ruby 1.9.2, and install the bundler gem>
    bundle install
    nanoc compile

That will compile the site and make it available in the public/ folder. You
can use `nanoc view` to setup a ad-hoc web server to view the site.

To publish the project on github pages, use the `rake publish` task.

[nanoc]: http://nanoc.stoneship.org/
