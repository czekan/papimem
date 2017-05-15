papimem
=======

Python API Request-Response Memorizer and Analizer

Papimem can handle requests made with [urllib](https://docs.python.org/3/library/urllib.html), 
[requests](docs.python-requests.org/en/master/) or any other library that can be configured to use proxy server.

Papimem can be used to store and analyze request being made from your application. It can be also used for mocking exisiting APIs.

Papimem utilize 

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
 --proxy_port  Proxy server http and https port to run on.
 --storage_dsn Persistent storage DSN for requests and responses.
 --mock_mode/--no-mock_mode  Run on mock mode (request are served from storage) or pass them to remote host and store.'


Run help:
```
(env)$ papimem --help
```
