# docker-php
PHP Docker image built with Debian Jessie.

This is a PHP image that can be used for general PHP development as well as
usage as a web server since it has php5-fpm installed.

It does have xdebug installed, although it is disabled by default since it
shouldn't be enabled for production. You can enable it by adding
`extension=xdebug.so` in a development.ini. See below to read more about
environment INI files.

## Environment Vars

### APP_ENVIRONMENT

This `APP_ENVIRONMENT` environment variable is used to link in potential INI
overrides before running any PHP commands. See the Environment INI Files
section below for more information.

## Environment INI files.
There is an entrypoint shell script for this image that will look for a PHP INI
file in this location: `/etc/php5/custom.conf.d/${APP_ENVIRONMENT}.ini`

If it finds an INI file in that location then it will link it into all the
conf.d directories before running any command you may pass to the docker image.

All you need to do to set up custom environment configs is add them to a
directory in the base of your repo like so:

* php.custom.ini.d/
    * development.ini
    * staging.ini
    * testing.ini
    * production.ini

You only need to specify environments with values you'd like to override since
it will only link the INI if the file exists.
