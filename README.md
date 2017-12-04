# Phase 2 - Back testing on Zerodha Kite platform

( This is in continuation to the back testing documentation  ( https://github.com/tomtillo/BackTesting ))

### Getting your API keys
From https://kite.trade , use your credentials to create an app  ( you should already have atleast Rs.2000/- in your credits for getting your trading API , and an additional Rs.2000/- for access to your historic API )
![](https://github.com/tomtillo/Zerodha/blob/master/Create.JPG)

Once you create your App , with the relevant details, you have access to your API key and the secret Key 
![](https://github.com/tomtillo/Zerodha/blob/master/App_details.JPG)


Clicking on your API key will reveal your API secret key.
![](https://github.com/tomtillo/Zerodha/blob/master/api_key_1.JPG)


## Steps involved in setting up a real time trading algorithm on zerodha - Kite
###  Step 1 - Install kiteconnect
```
pip install kiteconnect
```
###  Step 2 - Execute connect code using iPython
IPython is the easiest way to run your code - ( you will see later why )

```
from kiteconnect import KiteConnect
kite = KiteConnect(api_key="api_key_here")
kite.login_url()
```
This is the url you can use to get your access token. 

Enter your request token and your API secret here :
```
user = kite.request_access_token(request_token="request_token_here",
                                     secret="api_secret_key_here")
```

## Executing a Websocket connection - for live streaming 
Here - we can try with that of Reliance Industries:-738561

```
from kiteconnect import WebSocket

kws = WebSocket("apikey_here", "public_tocken_here", "clinet_id_here")
def on_tick(tick, ws):
    print(tick)

def on_connect(ws):
    ws.subscribe([738561, 5633])
    ws.set_mode(ws.MODE_FULL, [738561])

kws.on_tick = on_tick
kws.on_connect = on_connect
kws.enable_reconnect(reconnect_interval=5, reconnect_tries=50)
kws.connect()

```
Output of the streaming results :  ( you can funnel it to any of your web applications )
![](https://github.com/tomtillo/Zerodha/blob/master/web_socket.JPG)

## Common Errors
1. TokenException: Invalid session credentials
Reasons : 
1) Your token session is expired  ( re-connect using the api key and get the new token )
2) KeyError: 'access_token'

## Other ways of seam-less connections

There are other couple of seam-less connection which can be run as cron-jobs or as triggers running on the server . More details in the next github page - 
