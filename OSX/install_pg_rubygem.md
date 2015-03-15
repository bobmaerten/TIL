# How to install pg rubygem on OSX

`pg` gem searches for `pg_config` during installation, so you must have some sort
postgresql installation somewhere.

The fastest way to achieve this is to use `brew`:

    $ brew install postgres

Then install the `pg` gem with location of the pg_config binary:

    $ gem install pg -- --with-pg-config=/usr/local/bin/pg_config
