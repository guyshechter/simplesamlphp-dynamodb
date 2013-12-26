simplesamlphp-dynamodb
======================

**This distribution adds a DynamoDB storage class to simpleSAMLphp.**

### Overview
 
I've found it to be useful when running a PHP application that requires SAML authentication on a 
cluster of webservers behind an elastic load balancer on Amazon Web Services. Why set up a memcache cluster when
you can just as easily store your key-value pairs to DynamoDB?

### Installation

The file dynamodb_diff.txt includes a patch which should be applied to the source code for simplesamlphp-1.11-0.

1. Download the source from: http://code.google.com/p/simplesamlphp/downloads/list

2. Unpack the tar.gz file into a local directory ( ie ./simplesamlphp-1.11.0/ )

3. Download the patch (dynamodb_diff.txt) and copy into the simplesamlphp-1.11.0/ directory

4. cd into the source directory (simplesamlphp-1.11.0/)and apply the patch:

        src $ cd simplesamlphp-1.11.0/
        simplesamlphp-1.11.0 $ patch -p1 < dynamodb_diff.txt

5. You should see confirmation that 3 files were patched:

        patching file config/config.php
        patching file lib/SimpleSAML/Store/DynamoDB.php
        patching file lib/SimpleSAML/Store.php

6. Edit config/config.php in order to ensure that

        'store.type' => 'dynamodb',

7. If you need to modify any of the other configuration settings then search for the store.dynamodb.* variables:

        /*
         * The AWS_ACCESS_KEY_ID and AWS_SECRET_KEY for accessing DynamoDB.
         * You can chose to omit these if your AWS EC2 instance is provisoned with an IAM Instance Role.
         */
        'store.dynamodb.aws_key' => NULL,
        'store.dynamodb.aws_secret' => NULL,

        /*
         * The prefix for the table name.
         */
        'store.dynamodb.prefix' => 'myapp_simpleSAMLphp',

        /*
         * The region in which the table should be created.
         *
         * See http://docs.aws.amazon.com/aws-sdk-php/latest/class-Aws.Common.Enum.Region.html
         * for list of available regions.
         * Should be one of :us-east-1, ap-northeast-1, sa-east-1, ap-southeast-1, ap-southeast-2,
         * us-west-2, us-gov-west-1, us-west-1, cn-north-1, eu-west-1.
         */
        'store.dynamodb.region' => 'us-east-1',

        /*
         * The Read and Write capacity for the DynamoDB Table.
         *
         * See http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ProvisionedThroughputIntro.html
         */
        'store.dynamodb.readCapacityUnits' => 5,
        'store.dynamodb.writeCapacityUnits' => 5,
