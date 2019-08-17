Barker
======

Barker is a python module for notifying other servers using the webhook protocol. Webhooks are a way for a web server to communicate out to another server without direct user interaction. They can be used for notifications or triggers to start other services.

To use Barker, initialize the `Webhook` object:

```
from barker import Webhook
hook = Webhook()
```

The `Webhook` object has a number of attributes set by the user:

1. `url`: the url you want to send the webhook notification
2. `data`: the information you want to post in the webhook
3. `timeout`: the number of seconds to wait for a server response
4. `key`: the hashing key used to verify message data. If not given, it defaults to `BARKER`.

Additionally, some attributes are set by Barker:

1. `headers`: custom HTTP headers containing information for message verification (`BARKER_SIGNATURE` and `BARKER_TIMESTAMP`)
2. `response`: the response received from the server as a `requests.Response` object

When a webhook is sent, it will include a signature in a header (`BARKER_SIGNATURE`) that is an HMAC hash of the time the webhook was generated (also a header, `BARKER_TIMESTAMP`) and the data joined by a ";". Local verification ensures the message is both correct and current. Note that hashing is based on escaped unicode characters.
