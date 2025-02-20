Disclaimer: Please note that we no longer support older versions of SDKs and Modules. We recommend that the latest versions are used.

# README

# Contents

- Introduction
- Prerequisites
- Using the Gateway SDK
- License

# Introduction

This PHP SDK provides an easy method to integrate with the payment gateway.
 - The gateway.php file contains the main body of the SDK.
 - The sample code can be found in our integration guides and is intended as a minimal guide to demonstrate a complete 3DSv2 authentication process.

# Prerequisites
- The SDK requires the following prerequisites to be met in order to function correctly:
    - PHP 5.4+
    - SSL **NB: HTTPS is expected to be in place when using direct integration as the payment gateway will respond over SSL. Failure to provide an environment where HTTPS traffic is possible, will result in the SDK failing***

> Please note that we can only offer support for the SDK itself (gateway.php). While every effort has been made to ensure the sample code is complete and bug free, it is only a guide and cannot be used in a production environment.

# Using the Gateway SDK
Include the source code and set the static fields Merchant ID and secret key.

```
require('gateway.php');
use \P3\SDK\Gateway;
Gateway::$merchantID = '100856';
Gateway::$merchantSecret = 'Circle4Take40Idea';
```

The other static public variables of the class can also be overridden if required, including support for HTTP proxying if required. Take a look at gateway.php to see the full method signatures. A request array that describes the transaction is then required. For example:

```
    $req = array(
        'merchantID' => 100001,
        'action' => 'SALE',
        'type' => 1,
        'currencyCode' => 826,
        'countryCode' => 826,
        'amount' => 1001,
        'cardNumber' => '4012001037141112',
        'cardExpiryMonth' => 12,
        'cardExpiryYear' => 15,
        'cardCVV' => '083',
        'customerName' => 'Test Customer',
        'customerEmail' => 'test@testcustomer.com',
        'customerAddress' => '16 Test Street',
        'customerPostCode' => 'TE15 5ST',
        'orderRef' => 'Test purchase',
        // The following fields are only mandatory for 3DS v2 direct integration
        'remoteAddress' => $_SERVER['REMOTE_ADDR'],
        'threeDSRedirectURL' => $pageUrl . '&acs=1'
    );
```

> NB: This is a sample request. The gateway features many more options. Please see our integration guides for more details.

Then, depending on the integration method, you'd either call:

```
Gateway::directRequest($req);
```

OR

```
Gateway::hostedRequest($req);
```

And then handle the response received from the gateway.

License
----
MIT

**Disclaimer**

Sample code, SDKs and modules have been created as reference material only. Modules are developed and tested against vanilla base platform installs only. Any further module compatibility would need to be tested by the user/merchant/developer. Version support is as shown within the associated VERSION section. All sample code, SDKs and modules offer foundation transaction functionality for merchant and developers to use as a guide and/or to adapt, enhance or otherwise build upon. For the avoidance of doubt, this means that some desired functionality may not be useable or exist. All sample code, SDKs or modules that are used will require complete full end to end testing by the user/merchant/developer. Further to this, use of any sample code, SDKs or modules, Cardstream bears no responsibility for; nor extends any warranty in regard to; nor accepts any liability arising due to any changes or errors in functionality that may result. Developers, merchants or other users of any sample code, SDKs or modules accept these conditions de facto upon usage.
