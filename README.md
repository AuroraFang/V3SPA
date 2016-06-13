V3SPA Angularized
=================
## Requirements

- nodejs
- npm
- python
- pip
- mongodb
- setools

To set up the environment:

    $ # OS X
    $ brew install node

    $ # Fedora
    $ sudo yum install gcc nodejs npm python-tornado python-pip git python-devel mongodb-server
    $ sudo pip install virtualenv
    $ mkdir vespa && cd vespa
    $ git init
    $ git clone http://gitlab.labs/v3spa/ide.git
    $ cd ide
    $ git submodule update --init
    $ sudo npm install -g gulp
    $ sudo npm install
    $ virtualenv vespa
    $ source vespa/bin/activate
    $ pip install -r requirements.txt

To run sesearch you will need the following:

    $ # Fedora
    $ sudo dnf install bison flex gcc libsepol-devel libsepol-static libselinux-devel policycoreutils-python3 python3-networkx swig bzip2-devel redhat-rpm-config python3-qt5
    $ sudo pip install networkx

## Building

All of the assets are now served from static/, but they aren't
actually stored there. The Grunt build system is responsible for
compiling assets and putting them in the right place.

To build assets:

    $ cd external/d3hive
    $ sudo npm install
    $ gulp
    $ cd -
    $ gulp

## Layout

All of the client side code is now located in src/. All external
libraries are in external.

## Database

Mongo is installed at this point, but you need to create a location
for database storage. Then launch Mongod.
(Assuming you are in vespa directory.)

    $ mkdir ./mongodb

## Running

Mongo and two more binaries need to be launched.
(Assuming you are in the vespa dirrectory.)

    $ mongod --dbpath ./mongodb &
    $ python ide/vespa.py &
    $ (cd tmp/bulk && ../../api/bin/lobster-server) &

## Misc
At this point you should create the appropriate firewall rules for 
your machine to allow external access to port 8080 if you would like
the service open to other clients.

## Automated Install

There is a vagrant file and shell script provided to execute all the steps
during provisioning without launching Mongo or the two binaries at the end.