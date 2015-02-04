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

This can then be uploaded to an apt repository or installed directly
with a `dpkg -i`.


What it Does
------------

`au new` makes a new directory, and checks out the source repo you pass
to it into <projectname>/src.

Running `au release` will package the app up with its gem dependencies
(via bundler) such that it will install to /srv/<projectname>.

The `au release` command will add a date-based tag to HEAD of whatever
branch is checked out in the `src` directory.  The package name uses the
tag to specify the package version for Debian.

This process uses whichever ruby you currently have active, and because
binary gems are invariably involved, this needs to be the same ruby
you're deploying to.

You also need to build on the same distribution you're going to deploy
to, otherwise linking to native libraries isn't going to work.

To gather the dependencies for the package, `au release` finds first the
package for the ruby you're using, then the dependencies for any binary
gems in your app's $GEM\_HOME.

Note that this means your local ruby *must* have been installed by
apt-get, and must have the same package name as the ruby you'll be
using in production.

In addition, if there's a file called "depends" in your rails root, `au
release` expects it to list additional apt dependencies which scanning
the binary gems won't find.

Note that the .deb produced pays no attention whatsoever to the Debian
Packaging Guidelines: it does what it does to build the simplest
possible thing that can work.

Finally, there's also an `au clean` command, which will clear out the
build/ and pkg/ directory.  Use this when things seem not to be working.


What it Doesn't Do
------------------

`au` makes no claims to know how you're going to run your application,
so doesn't build Procfiles, have any init.d scripts, or do whatever it
would be that systemd wants.  All it does is get your app, and all its
dependencies, onto the server.  The rest is up to you (but I'm a fan of
runit and puma).


Author
------

Alex Young <alex@bytemark.co.uk>
