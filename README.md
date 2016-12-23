# google-home-notifier
Send notifications to Google Home

#### Installation
```sh
$ npm install google-home-notifier
```

#### Usage
```javascript
var googlehome = require('google-home-notifier');

googlehome.device('Google Home'); // Change to your Google Home name
googlehome.notify('Hey Foo', function(res) {
  console.log(res);
});
```

#### Listener
If you want to run a listener look at the example.js. You can run this from a Raspberry Pi, pc or mac. The example uses ngrok so the server can be reached from outside your network. I tested with ifttt.com Maker channel and it worked like a charm

```sh
$ git clone https://github.com/noelportugal/google-home-notifier
$ cd google-home-notifier
$ npm install
$ node example.js
POST "text=Hello Google Home" to:
    http://localhost:8080/google-home-notifier
    https://xxxxx.ngrok.io/google-home-notifier
example:
curl -X POST -d "text=Hello Google Home" https://xxxxx.ngrok.io/google-home-notifier
```
#### Raspberry Pi
If you are running from Raspberry Pi make sure you have the following packages:
```sh
sudo apt-get install git-core libnss-mdns libavahi-compat-libdnssd-dev
```
Then you will have to modify the folowing file "node_modules/mdns/lib/browser.js"
```sh
vi node_modules/mdns/lib/browser.js
```
Find the following:
```javascript
Browser.defaultResolverSequence = [
  rst.DNSServiceResolve(), 'DNSServiceGetAddrInfo' in dns_sd ? rst.DNSServiceGetAddrInfo() : rst.getaddrinfo()
, rst.makeAddressesUnique()
];
```
Change to:
```javascript
Browser.defaultResolverSequence = [
  rst.DNSServiceResolve(), 'DNSServiceGetAddrInfo' in dns_sd ? rst.DNSServiceGetAddrInfo() : rst.getaddrinfo({families:[4]})
, rst.makeAddressesUnique()
];
```


