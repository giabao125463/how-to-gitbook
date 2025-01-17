# Authentication

To ensure secure access to the Nami Exchange API, all requests must be authenticated using API keys. Follow the steps below to [register an account](authentication.md#create-an-account), complete [KYC verification](authentication.md#complete-kyc-verification), [enable 2FA](authentication.md#enablle-two-factor-authentication-2fa), and [generate your API key](authentication.md#generate-an-api-key).

### Create an Account

You'll need a Nami Exchange account to use the API. Follow these steps to register:

1. **Visit the Registration page**: Go to [Nami Exchange Registration](https://auth.nami.io/register).
2. **Fill out the Registration form**: Provide the necessary information, including email address, and password.
3. **Verify your Email**: After submitting the registration form, check your email for a verification link. Click the link to verify your email address.
4. **Log in**: Once your email is verified, log in to your account using your credentials.

### Complete KYC Verification

KYC (Know Your Customer) verification helps ensure a secure trading environment. Here's how to complete it:

1. **Locate KYC verification:** Navigate to your account settings and find the dedicated KYC verification section.
2. **Submit required documents**: Provide the necessary documentation, such as a government-issued ID and proof of address. These documents help verify your identity and protect against fraudulent activity.
3. **Wait for approval**: The verification process may take some time. You will be notified via email once your KYC is approved.

More detailed instructions: [here](https://nami.exchange/support/faq/tutorials/kyc-on-nami-exchange)

### Enablle Two-Factor Authentication (2FA)

For enhanced security, you need to enable Two-Factor Authentication (2FA). Follow these steps:

1. **Navigate to Security settings**: Go to your account settings and locate the Two-Factor Authentication (2FA) section.
2. **Enable 2FA**: Follow the instructions to enable 2FA, typically involving scanning a QR code with an authenticator app (such as Google Authenticator) and entering the generated code.

More detailed instructions: [here](https://nami.exchange/support/faq/account-functions/create-two-factor-authentication-2fa)

### Generate an API Key

After registering, completing KYC verification, and enabling 2FA, you can generate an API key:

1. **Navigate to API settings**: Go to your account settings and locate the API settings section.
2. **Generate new API Key**: Click the "Generate API Key" button. Your new API key will be displayed. Copy this key and store it securely. You will need it to authenticate your API requests.

{% hint style="info" %}
By following these steps, you can generate an API key for Spot Trading on Nami Exchange. Make sure to keep your API key secure and only use it from authorized IP addresses if you have set any restrictions.
{% endhint %}

### Authentication using API key <a href="#authentication-using-api-key" id="authentication-using-api-key"></a>

Authentication is done by sending the following HTTP headers:

* **apiKey**: Your public API key (pass through the request's header "x-api-key")
* **apiSecret**: Your API secret key (use to hash query)
* **api-signature**: A signature of the request you are making. It is calculated as hex(HMAC\_SHA256(apiSecret, queryString). See the example calculations below.\
  `Hint: queryString is make from your query params (it doesn't need query data) and the timestamp you execute the request.`\


**Example**

<pre class="language-sh"><code class="lang-sh">apiKey = 'N3LbmwMAXcObdVYdP8KTMYjsi94CUpEh8C3F2xhDKdxbkfQn8Bi3FQP7LudeN9Vb'
apiSecret = 'UNCZHD1e4501X1WGO9PqjGJBDqWoNjUlc05YZTy38t9Wd7rHWmrmtfKfb1Vpb5RH'


Simple GET 
Get user wallet balance from `/api/v4/user/balance`

method = 'GET'
url = `/api/v4/user/balance`
params = {
    type: '0' # Type 0 mean Spot wallet
}
data = {}
<strong>
</strong>Get current timestamp:
<strong>    timestamp = 1721284769720 # Thursday, July 18, 2024 6:39:29.720 AM
</strong>
Create query string:
    queryString = 'type=0&#x26;timestamp=1721284769720'

Create signature:
    signature = 'CryptoJs.HmacSHA256(queryString, apiSecret).toString()'
<strong>    signature = '2cc8df81fc34801e6b6f7dbaf79e72ab098bf5461973239689e32e71368cd145'
</strong>    
Full query:
    path = '/api/v4/user/balance?type=0&#x26;timestamp=1721284692786&#x26;signature=2cc8df81fc34801e6b6f7dbaf79e72ab098bf5461973239689e32e71368cd145'

Full request:
    curl --location 'https://nami.exchange/api/v4/user/balance?type=0&#x26;timestamp=1721284769720&#x26;signature=2cc8df81fc34801e6b6f7dbaf79e72ab098bf5461973239689e32e71368cd145' \
    --header 'x-api-key: N3LbmwMAXcObdVYdP8KTMYjsi94CUpEh8C3F2xhDKdxbkfQn8Bi3FQP7LudeN9Vb' \

   

Simple POST
Create new Order from '/api/v4/spot/order'

method = 'POST'
url = '/api/v4/spot/order'
params = {
    symbol: 'NAMIVNDC',
    side: 'SELL',
    type: 'LIMIT',
    quantity: 50000,
    price: 600,
}

Get current timestamp:
    timestamp = 1721284021975 # Thursday, July 18, 2024 6:27:01.975 AM
    
Create query string:
    queryString = 'symbol=NAMIVNDC&#x26;side=SELL&#x26;type=LIMIT&#x26;quantity=50000&#x26;price=600&#x26;timestamp=1721284021975'
    
Create signature:
    signature = 'CryptoJs.HmacSHA256(queryString, apiSecret).toString()'
    signature = '87455e30b15d4d2fe234eeec92cfc165f8b8647bf583ce09f0bdb6b3c6a09b77'

Full query:
    path = '/api/v4/spot/order?symbol=NAMIVNDC&#x26;side=SELL&#x26;type=LIMIT&#x26;quantity=50000&#x26;price=600&#x26;timestamp=1721284021975&#x26;signature=87455e30b15d4d2fe234eeec92cfc165f8b8647bf583ce09f0bdb6b3c6a09b77'

Full request:
    curl --location --request POST 'https://nami.exchange/api/v4/spot/order?symbol=NAMIVNDC&#x26;side=SELL&#x26;type=LIMIT&#x26;quantity=50000&#x26;price=600&#x26;timestamp=1721284021975&#x26;signature=87455e30b15d4d2fe234eeec92cfc165f8b8647bf583ce09f0bdb6b3c6a09b77' \
    --header 'Content-Type: application/json' \
    --header 'x-api-key: N3LbmwMAXcObdVYdP8KTMYjsi94CUpEh8C3F2xhDKdxbkfQn8Bi3FQP7LudeN9Vb' \
</code></pre>
