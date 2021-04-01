## ZOO Kernel PHP Support {#zoo_kernel_php_support}

## What\'s a ZOO PHP Service Provider looks like ? {#whats_a_zoo_php_service_provider_looks_like}

It is a combinaison of a PHP script and multiple metadata configuration
files (zcfg).

## First example {#first_example}

Our first example is a basic HelloWold service which outputs a string
containing an inputed string and a Hello World message.

The code can be found
[here](http://trac.zoo-project.org/browser/trunk/zoo-services/hello-php/hello.php).

The metadata configuration file is
[here](http://trac.zoo-project.org/browser/trunk/zoo-services/hello-php/cgi-env/HelloPHP.zcfg).

## How to deploy such a Service Provider {#how_to_deploy_such_a_service_provider}

Simply copy the zcfg and the PHP script in your cgi-bin directory or
whatever metapath you want.

