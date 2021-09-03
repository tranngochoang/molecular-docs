# Documentation for Molecular DNA

The documentation here is built using Jekyll, which allows a static site to be built
using markdown.

Pushing this repository to the master branch will (one day) trigger a build of the
website and documentation.

The site can be viewed locally by calling:
```
bundle install  # if you haven't already
bundle exec jekyll serve
```

This packages requires Ruby to be installed.

Instructions on how to update the docs are at https://pmarsceill.github.io/just-the-docs/

Updating the configuration macro documentation.

1. Make a Geant4 macro `get_commands.mac` which extracts all possible commands as follows:
```
/control/manual /world
/control/manual /analysisDNA
/control/manual /dnageom
/control/manual /cell
```
2. Run `molecular -t 1 -m get_commands.mac` > commands.txt
3. Run `python g4command_processor.py commands.txt --markdown`
4. Copy the stdout output to the Configuration markdown file.
