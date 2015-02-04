au
==

A tool for debian-packaging Rails apps from git repositories.

Quick Start
-----------

    $ au new projectname git@host:project/name.git
    $ cd projectname
    $ au release
    $ ls pkg/*.deb
    pkg/projectname_2015020401_amd64.deb

This can then be uploaded to an apt repository or installed with a 
`dpkg -i`.

What it Does
------------

`au new` makes a new directory, and checks out the source repo you pass
to it into <projectname>/src.

Running `au release` will package the app up with its gem dependencies
(via bundler) such that it will install to /srv/<projectname>.

The `au release` command will add a date-based tag to HEAD of whatever
branch is checked out in the `src` directory.  The package name uses the
tag to specify the package version for Debian.


Author
------

Alex Young <alex@bytemark.co.uk>
