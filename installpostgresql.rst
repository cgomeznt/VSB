Linux downloads (Debian)
=========================

PostgreSQL is available in all Debian versions by default. However, the stable versions of Debians "snapshot" a specific version of PostgreSQL that is then supported throughout the lifetime of that Debian version. The PostgreSQL project also maintains an apt repository with all supported of PostgreSQL available.

PostgreSQL Apt Repository
If the version included in your version of Debian is not the one you want, you can use the PostgreSQL Apt Repository. This repository will integrate with your normal systems and patch management, and provide automatic updates for all supported versions of PostgreSQL throughout the support lifetime of PostgreSQL.

The PostgreSQL apt repository supports the currently supported stable versions of Debian::

  bookworm (12.x)
  bullseye (11.x)
  buster (10.x)
  sid (unstable)
  
on the following architectures::

  amd64
  arm64
  i386 (buster and older)
  ppc64el
  
To use the apt repository, follow these steps:

Create the file repository configuration::

  sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

Import the repository signing key::

  wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc |  apt-key add -

Update the package lists::

  apt-get update

Install the latest version of PostgreSQL.
If you want a specific version, use 'postgresql-12' or similar instead of 'postgresql'::

  apt-get -y install postgresql

Included in distribution
-------------------------

Debian includes PostgreSQL by default. To install PostgreSQL on Debian, use the apt-get (or other apt-driving) command::

  apt-get install postgresql-12
  
The repository contains many different packages including third party addons. The most common and important packages are (substitute the version number as required):

postgresql-client-12	client libraries and client binaries

postgresql-12	core database server

libpq-dev	libraries and headers for C language frontend development

postgresql-server-dev-12	libraries and headers for C language backend development
