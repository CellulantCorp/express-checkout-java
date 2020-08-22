## Getting started

You first need to create an account on our sandbox on this [link](https://developer.tingg.africa/checkout/v2/portal/#/register/user) to get the credentials to enable you successful integrate to checkout. The credentials include the access key, IV key and Secret Key.

## Encrypt params with Java to render checkout

Capture the params and package them into a json object

``` java
```
            JSONObject parametersObject = new JSONObject();
           
            //add the parameters
            parametersObject.put("merchantTransactionID", YOUR_UNIQUE_TRANSACTION_ID);
            parametersObject.put("customerFirstName", "Customer first Name");
            parametersObject.put("customerLastName", "Customer last Name");
            parametersObject.put("amount", AMOUNT_TO_CHARGE);
            parametersObject.put("MSISDN", "254722100200");
            parametersObject.put("currency", "CURRENCY_CODE");
            parametersObject.put("serviceDescription", "Test Transaction");
            parametersObject.put("countryCode", "COUNTRY_CODE");
            parametersObject.put("customerEmail", "john.die@domain.com");           
            parametersObject.put("language", "en");            
            parametersObject.put("accountNumber", "ACCOUNT_NUMBER");
            parametersObject.put("successRedirectUrl", "http://localhost/tingg-checkout/success.php");
            parametersObject.put("failRedirectUrl", "http://localhost/tingg-checkout/failed.php");
            parametersObject.put("paymentWebhookUrl", "http://localhost/tingg-checkout/payment_webhook.php");
            parametersObject.put("serviceCode", YOUR_SERVICE_CODE);
            parametersObject.put("accessKey", ACCESS_KEY);
            parametersObject.put("payerClientCode", "");
            parametersObject.put("dueDate", "2020-08-20 14:00:59");

            //------ add other necessary parameters and do the necessary safety precautions like

            byte[] encryptedParams = Encrypt.encryptString(
                    IV_KEY,
                    SECRET_KEY,
                    parametersObject.toString()
            );
            
            String params = Encrypt.bytesToHex(encryptedParams);
            
            ...
            ```

## Render checkout
```
...
String checkOutUrl = "https://developer.tingg.africa/checkout/v2/express/";
        
checkOutUrl = checkOutUrl.concat("?")
                .concat("countryCode=" + Constants.COUNTRY_CODE)
                .concat("&accessKey=" + Constants.ACCESS_KEY)
                .concat("&params=" + params);
...
```

Proceed to render the checkout URL above in your browser
