
This distribution adds a DynamoDB storage class to simpleSAMLphp.

Author: Guy Shechter
Date  : December 26, 2013

I've found it to be useful when running a PHP application that requires SAML authentication on a 
cluster of webservers behind an elastic load balancer on Amazon Web Services. Why set up a memcache cluster when
you can just as easily store your key-value pairs to DynamoDB?

The file dynamodb_diff.txt includes a patch which should be applied to source code for simplesamlphp-1.11-0.

Patch deployment instructions:

1) Download the source from: http://code.google.com/p/simplesamlphp/downloads/list
2) Unpack the tar.gz file into a local directory ( ie ./simplesamlphp-1.11.0/ )
3) Download the patch (dynamodb_diff.txt) and copy into the simplesamlphp-1.11.0/ directory
3) cd into the source directory (simplesamlphp-1.11.0/)and apply the patch:

	simplesamlphp-1.11.0 $ patch -p1 < dynamodb_diff.txt

4) You should see confirmation that 3 files were patched:

	patching file config/config.php
	patching file lib/SimpleSAML/Store/DynamoDB.php
	patching file lib/SimpleSAML/Store.php

5) Edit config/config.php in order to ensure that 'store.type' => 'dynamodb'. If you need to modify the default
configuration settings then search for the store.dynamodb.* variables
