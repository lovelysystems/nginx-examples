===========================================
S3 Authentication Proxy Example using Nginx
===========================================

This is a short example on how to create a transparent authentication
proxy to a private s3 bucket.

The main feature used is the set-misc-module's set_hmac_sha1 and
set_encode_base64 directives. Take a look at the example config file
template in ``nginx/nginx.conf.in``.

Setup (MAC)
===========

Your environment will need to contain your AWS credentials in the following
two environment variables: ``AWS_ACCESS_KEY`` and ``AWS_SECRET_KEY``.

Additional required libraries to the ones need to build nginx are
openssl and lua.

Also this example uses buildout to download and build nginx with all
required modules, which requires a python interpreter.

Run bootstrap::

 python bootstrap.py --distribute

And run buildout::

 ./bin/buildout

If your AWS credentials change after running the buildout initially,
you need to re-run the buildout.

Testing
=======

After the build you can start nginx in the foreground with::

 ./bin/nginx

The generated config file resides in ``./nginx/nginx.conf``

To issue a get request via curl to your s3 bucket use the following
url pattern::

 curl http://localhost:19999/<bucket-name>/<path-to-object>

