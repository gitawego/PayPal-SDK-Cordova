# PayPal SDK Cordova Plug-in

Integration
-----------
##Requirement

###Android
- Download the [PayPal Android SDK](https://github.com/paypal/PayPal-Android-SDK).
- Read the [Android Integration Guide](https://developer.paypal.com/webapps/developer/docs/integration/mobile/android-integration-guide/) for
   conceptual information that will be useful during integration.
- Follow the "Initial setup" instructions in the [Android Integration Guide](https://developer.paypal.com/webapps/developer/docs/integration/mobile/android-integration-guide/) to add the
   required files, acknowledgments and `AndroidManifest.xml` modifications to your app.

###IOS
- Download the [PayPal iOS SDK](https://github.com/paypal/PayPal-iOS-SDK)
- Read the [iOS Integration Guide](https://developer.paypal.com/webapps/developer/docs/integration/mobile/ios-integration-guide/) for
   conceptual information that will be useful during integration.
- Follow the "Initial setup" instructions in the [iOS Integration Guide](https://developer.paypal.com/webapps/developer/docs/integration/mobile/ios-integration-guide/) to add the
   required files, linker flags, frameworks, and acknowledgments to your app.

##Installation
install it via cordova cli:
```
cordova plugin add https://github.com/gitawego/PayPal-SDK-Cordova.git
```



Sample code
-----------

```javascript

// for simplicity we have defined a simple buyButton in our index.html
// `<button id="buyButton" disabled>Buy Now!</button>`
// and we defined a simple onclick function in our `deviceready` event
var buyButton = document.getElementById("buyButton");
buyButton.onclick = function(e) {

  // See PayPalMobilePGPlugin.js for full documentation
  // set environment you want to use
  window.plugins.PayPalMobile.setEnvironment("PayPalEnvironmentNoNetwork");

  // create a PayPalPayment object, usually you would pass parameters dynamically
  var payment = new PayPalPayment("1.99", "USD", "Awesome saws");
  
  // define a callback when payment has been completed
  var completionCallback = function(proofOfPayment) {
    // TODO: Send this result to the server for verification;
    // see https://developer.paypal.com/webapps/developer/docs/integration/mobile/verify-mobile-payment/ for details.
    console.log("Proof of payment: " + JSON.stringify(proofOfPayment));
  }

  // define a callback if payment has been canceled
  var cancelCallback = function(reason) {
    console.log("Payment cancelled: " + reason);
  }
  
  // launch UI, the PayPal UI will be present on screen until user cancels it or payment completed
  window.plugins.PayPalMobile.presentPaymentUI("YOUR_CLIENT_ID", "YOUR_PAYPAL_EMAIL_ADDRESS", "someuser@somedomain.com", payment, completionCallback, cancelCallback);
}
```
