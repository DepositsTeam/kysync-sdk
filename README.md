# Deposits KySync Web SDK



The Deposits KySync SDK enables financial services to embed identity verification to new or existing onboarding workflows. This SDK uses the Kysync API services from Deposits. You can get API keys from your Deposits program on the console, [here](https://launch.new) or view the sandbox [here](https://kysync-web.deposits.dev/).

  

## To Initiate the SDK
You have to first import our Javascript SDK. We have created examples that can guide you on sandbox and production.

#### Example

Example in sandbox
```sh
https://api.deposits.dev/example/kysync
```
Example in production
```sh
https://api.ondeposits.com/example/kysync
```

#### How to use

SDK Url and JS Import in sandbox
```sh
https://api.deposits.dev/sdk/kysync.js

<script src="https://api.deposits.dev/sdk/kysync.js"></script>
```
SDK Url and JS Import in production
```sh
https://api.ondeposits.com/sdk/kysync.js

<script src="https://api.ondeposits.com/sdk/kysync.js"></script>
```

The second line of code imports our SDK to your web page. With this, you can call the appropriate function to initiate the Deposits KySync flow.
  

Below is what an implementation of the `DepositsKysync` would look like:

```sh
<!DOCTYPE html>
<html lang=“en”>
<head>
  <title>KySync Demo</title>
</head>
<body>
    <div id="content">
        <div id="form">
            <div class="card">
                <div id="title">
                    <img src="https://assets.deposits.inc/img/logo/deposits_square/png/logo_main.png" alt="deposits.dev" />
                    <p id="reducedMargin" class="ui-heading heroNew h5">
                        Deposits KySync Demo
                    </p>
                </div>
                                <div class="text-center mt-5">
                    <h5>User could not be retrieved</h5>
                </div>
                                                <div class="text-center">
                    <h5>Business could not be retrieved</h5>
                </div>
                            </div>
        </div>
    </div>

    <script src="https://api.dev.deposits.dev/sdk/kysync.js"></script>
    <script>
        let public_key = ''
        document.getElementById("initiate_kyc").addEventListener("click", function(e) {
            public_key = document.getElementById("public_key").value;
            let access_id = document.getElementById("user_access_id").value;
            let entity_type = 'user'
            DepositsKysync({
                public_key,
                access_id,
                redirect_url: "https://ondeposits.com",
                entity_type,
                callback: (data) => {
                    console.log("callback", data);
                },
            });
        });
        document.getElementById("initiate_kyb").addEventListener("click", function(e) {
            public_key = document.getElementById("public_key").value;
            let access_id = document.getElementById("business_access_id").value;
            let entity_type = 'business'
            DepositsKysync({
                public_key,
                access_id,
                redirect_url: "https://ondeposits.com",
                entity_type,
                callback: (data) => {
                    console.log("callback", data);
                },
            });
        });
    </script>
</body>
</html>

```

```
document.getElementById("initiate_kyc").addEventListener("click", function (e) {
        // code
    }
)
```

This is an event listener that lets your webpage know when to call our SDK to initiate the KYC/KYB process. It tells the web page to initiate the KySync experience when the user clicks on the button, it is also possible to programatically click the button via a page load event or mouse move if you prefer to trigger the KySync process tourself.

`public_key = document.getElementById("public_key").value;`
`let access_id = document.getElementById("user_access_id").value;`
`let access_id = document.getElementById("business_access_id").value;`

Using the code above, we get the information about the program and the user or the business. 
The public key can be gotten from the program/tenant page of our Console while 
The user access id can be gotten from the endpoint below
```sh
{{baseUrl}}/user/refresh-kyc
```
The business access id can be gotten from the endpoint below
```sh
{{baseUrl}}/user/business/refresh-kyb
```
##### Base Url
Example in sandbox
```sh
https://api.deposits.dev/api/v2
```
Example in production
```sh
https://api.ondeposits.com/api/v2
```

```sh
DepositsKysync({
    public_key,
    access_id,
    redirect_url: "https://ondeposits.com",
    entity_type,
    callback: (data) => {
        console.log("callback", data);
    },
});
```

Calling the `DepositsKysync` function initiates the KySync process. This function becomes available in your code because of the script we imported initially. This function expects a single argument which is an object that gives the SDK all the information it needs to properly initiate KYC/KYB.
  
##### Successful KYC/KYB
If the KYC/KYB process is successful, a response similar to this will be gotten:

```
{
	“data”: {
		“public_key”: “”,
		“access_id”: “”
	},
	“message”: “KYC/KYB successful”,
	“status”: “success”
}
```

##### Callbacks & Redirects
After calling `DepositsKysync` and the KYC/KYB process is completed, what happens next?
There are two options to determine this.

1. Callbacks: With callbacks, you specify the Javascript function for us to call after the KYC/KYB process has been successful.

2. Redirects: If you specify a redirect_url like we specified in the example above, your customers will be directed to that URL after successful payment.

###### PS: 
It is important to note that a redirect takes precedence over a callback. What this means is that if a redirect_url is specified, it will be called rather than the callback.

##### Cancelled KYC/KYB
If the customer closes the KySync modal before making payment or clicks "Cancel", we'll cancel the KySync session, hide the modal, and you won't be notified. If you do want to be notified, though, you can specify an onclose function. We'll call this function if the KySync popup is cancelled.

  
#### Framework Integrations
The SDK is framework agnostic, it is universal for any Javascript framework. This SDK is written in pure Javascript, it can be used with any Javascript framework, like React, Vue, etc.
  

## Features

**Simplified Security**: We make it simple for you to collect sensitive data such as Social Security Number. This means the sensitive data is sent directly to Deposits instead of passing through your server.

  

## Contributing

Only members of the deposits team can contribute to this. You can create an issue if you find a bug or have any challenge using this SDK.
