# Rest API

#### Generating a Signature for API Requests

Before making a call to the Nami API, you need to generate a signature using your API secret. The signature ensures the integrity and authenticity of your request. Follow the steps below to generate the signature in JavaScript:

1.  **Add Timestamp**: Generate a timestamp to include in your request parameters.

    ```javascript
    paramsObject['timestamp'] = Date.now();
    ```
2.  **Prepare the Query String**: Convert the parameters object to a query string.

    ```javascript
    const queryString = new URLSearchParams(paramsObject).toString();
    ```
3.  **Generate the Signature**: Use the CryptoJS library or any other library to generate an HMAC SHA-256 signature using your query string and API secret.

    ```javascript
    const signature = CryptoJS.HmacSHA256(queryString, nami_api_secret).toString();
    ```
4.  **Set the Signature in Environment Variables**:

    ```javascript
    paramsObject['signature'] = signature;
    ```

\
Dive into the specifics of each API endpoint by checking out our complete documentation.

{% content-ref url="broken-reference" %}
[Broken link](broken-reference)
{% endcontent-ref %}

{% content-ref url="trading/close-order.md" %}
[close-order.md](trading/close-order.md)
{% endcontent-ref %}

{% content-ref url="trading/close-all-order.md" %}
[close-all-order.md](trading/close-all-order.md)
{% endcontent-ref %}

{% content-ref url="trading/get-order-open.md" %}
[get-order-open.md](trading/get-order-open.md)
{% endcontent-ref %}

{% content-ref url="trading/get-order-history.md" %}
[get-order-history.md](trading/get-order-history.md)
{% endcontent-ref %}

{% content-ref url="trading/get-order-trade-history.md" %}
[get-order-trade-history.md](trading/get-order-trade-history.md)
{% endcontent-ref %}

{% content-ref url="market-data/get-24h-ticker-price.md" %}
[get-24h-ticker-price.md](market-data/get-24h-ticker-price.md)
{% endcontent-ref %}

{% content-ref url="market-data/get-market-depth.md" %}
[get-market-depth.md](market-data/get-market-depth.md)
{% endcontent-ref %}

{% hint style="info" %}
If you receive an error, please check the table below to understand the error code and its meaning
{% endhint %}

{% content-ref url="../error-code.md" %}
[error-code.md](../error-code.md)
{% endcontent-ref %}
