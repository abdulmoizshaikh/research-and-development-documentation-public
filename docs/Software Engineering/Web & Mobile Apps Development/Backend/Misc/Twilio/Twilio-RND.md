# Twilio RND

### Phone verification

testing of twilio otp send and verification done 1 hour

key notes

Step 1: Create a Verification Service

Create a Service in one of two ways:

In the Twilio Verify Console

Using the API (code sample on this page)

A Verification Service is the set of common configurations used to create and check verifications. This includes features like:

Step 2: Send a Verification Token

This will send a token to the end user through the specified channel. Newly created verifications will show a status of pending. Supported channels are sms, call, and email

Step 3: Check the Verification Token

```bash showLineNumbers
Token Status in response
Correct approved
Incorrect pending
```

boilerplate project v2

https://github.com/TwilioDevEd/verify-v2-quickstart-node#twilio-account-settings

Twilio Verify Node.js Express Quickstart

https://www.twilio.com/docs you can search here
https://www.twilio.com/docs/verify
https://www.twilio.com/docs/verify/quickstarts/node-express

doc : https://www.twilio.com/docs/verify/api

for cred

https://www.twilio.com/console

create a service with friendly name like "otp-verification-service" here https://www.twilio.com/console/verify/services

https://www.youtube.com/watch?v=ekv6Xh_Im5c

for resending the code we use same method that is responsible for send the code

"Re-sending the Code

then uses the same instance function we defined earlier to resend the code.

https://www.twilio.com/docs/authy/tutorials/account-verification-node-express#code-resend-a-users-code

https://www.twilio.com/docs/authy/tutorials/account-verification-node-express#re-sending-the-code"

Resend OTP ki research ki hy mene twilio doesn't provide any separate event for this except we have to recall twilio service that is responsible for sending OTP code after register call so tha same otp will send again on that perticular device / number

I have tested it works fine we can do resend work from this event as well

## Twilio

1. **Stop Recurring Charges**

https://support.twilio.com/hc/en-us/articles/360010066814-Stop-Recurring-Charges

Note, you can avoid a low balance warning in the future by setting up [automatic replenishment](https://links.twiliocdn.com/ls/click?upn=3kZIcBV84MSbPEonqfrF6dGb3PJ6jbldw7J3yS57HqfbJ21yaO3Ttr8cpJrGvnbJ9xyK_68PNjfmRBr-2BjCI9mwzPeN9FFYWNeq74cUHODB7oiLJqsmPuEYN4tGnYZZDjR4VSb93PX-2B9z67E30yMdKClUPkV-2FFTR4iJXcBbIKejXoUsXEhNgVeOJxHgwmH5AVVU22nr7jdQzxxSQeb309dl8Wzm7hEHlc4OGn5nYrw3KXGVZuiMuG0O5NVH23e1nldXtPq9e2AScKj4Jt0vAjMfQo9eT8o6u8TfjqTNjvkvXQG3W0-3D) of your account when it gets low.

In case you are not using your Twilio account - please visit the [Stop Recurring Charges](https://links.twiliocdn.com/ls/click?upn=3kZIcBV84MSbPEonqfrF6U6w0vtD9NVUO-2BmIkGzUh7c6Ci3Xf6djwiNlsH3pvRVwcKTYRV5y64-2FFaeo9ef6KyW6G-2BQ4ZRP1FLAMZnTnqPBQU-2Fmve36QLaCSh2LEZ5iICp_x__68PNjfmRBr-2BjCI9mwzPeN9FFYWNeq74cUHODB7oiLJqsmPuEYN4tGnYZZDjR4VSb93PX-2B9z67E30yMdKClUPkQ97mb00bYm3z5j-2BHYK4NaqQ7l0hPUcL-2FViQDLNHWW7XeYgPfyGkVxejj9m8fEzbVzqTCLyqpo9Avpi6y777FxC5jM1Mqsqkyon5NJNpOI8c2PDSNggA6LnTb7lOyzGzydwhXUJ1CGVoHiDUEM976pY-3D) page or our

[How-to-close a Twilio account guide](https://links.twiliocdn.com/ls/click?upn=3kZIcBV84MSbPEonqfrF6U6w0vtD9NVUO-2BmIkGzUh7c6Ci3Xf6djwiNlsH3pvRVwqaFpnE40xi07AS5FtBqzBrIcgKuVNsfhG8BfM2njxnx8REZXc0vDLlrT8iHpMzm7-2BkZ9P77TVwXo5e8L0iJhYQ-3D-3DKL4t_68PNjfmRBr-2BjCI9mwzPeN9FFYWNeq74cUHODB7oiLJqsmPuEYN4tGnYZZDjR4VSb93PX-2B9z67E30yMdKClUPkYWufJSAoCFoJHK2FtG1uYErg7ZupgiyRAs4QDs-2FRua3X1X8eI64wRMwaZXbrlC4al7g8gcSnyWylUmCNMcTZCzaPvyB40QcFpRtQYRFKwPMsP6Gt2OOaiG83L279xRqEgViB7RLbnoHwVo1AbPggUM-3D).
