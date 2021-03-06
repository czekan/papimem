papimem
=======

Python API Request-Response Memorizer and Analizer

Papimem can handle requests made with [urllib](https://docs.python.org/3/library/urllib.html), 
[requests](docs.python-requests.org/en/master/) or any other library that can be configured to use proxy server.

Papimem can be used to store and analyze request being made from your application. It can be also used for mocking exisiting APIs.


## Requirements

papimem requires Python 3.5+


## Installation from pypi:

Install package with pip:
```
$ pip install papimem
```

## Installation from repository:

Clone repository:
```
$ git clone https://github.com/czekan/papimem
```

Create virtualenv with python 3.5+ in repository folder:
```
$ cd papimem && virtualenv env --python=/usr/bin/python3.6 && source env/bin/activate
```
You may need to alter python path in above command.

Install package with setuptools:
```
(env)$ pip setup.py install
```

## Usage:

Run in interactive mode
```
(env)$ papimem
```
or pass options in command line arguments
```
(env)$ papimem --proxy_port 8080 --storage_dsn=redis://localhost:6379/0 --no-mock_mode
```

Arguments:
 - --proxy_port  Proxy server http and https port to run on. default: 8080
 - --storage_dsn Persistent storage DSN for requests and responses. default: redis://localhost:6379/0
 - --mock_mode/--no-mock_mode  Run on `mock mode` - request are served from storage
                             or `no mock mode` - pass them to remote host and store.
                             default: --no-mock_mode

Run help:
```
(env)$ papimem --help
```

To use this app you need to configure your application so it uses Papimem as a proxy server.
For libraries like `requests` (and probably many others) you need to export environment variables `HTTP_PROXY`
and `HTTPS_PROXY` and point them to the running Papimem proxy.

You also need to add root/CA Certificate generated by mitmproxy library (located in ~/.mitmproxy/mitmproxy-ca.pem)
to your system CA bundle or at least for `requests` library you can set it as an environment variable `REQUESTS_CA_BUNDLE`.

```
(env)$ export HTTP_PROXY=localhost:8080
(env)$ export HTTPS_PROXY=localhost:8080
(env)$ export REQUESTS_CA_BUNDLE=~/.mitmproxy/mitmproxy-ca.pem
# run your app
(env)$ python -c "import requests; print(requests.get('https://jsonplaceholder.typicode.com/comments', params={'postId': 1})).text" 
```

By default Papimem runs a web app on `http://localhost:8090` where you can see all stored requests and responses.

If you want to use stored requests as a offline cache or mock simply run papimem with `--mock_mode` param.
