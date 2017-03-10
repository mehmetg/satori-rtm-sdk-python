# Python SDK for Satori Platform

Use the Python SDK for the Satori platform to create server-based applications 
that use the Satori to publish and subscribe.

# Installation

```
pip install satori-sdk-python
```

Secure WebSocket communication (``wss://``) is supported 
for Python 2.7.9+ and PyPy 2.6+ only.

## Optional dependencies

### rapidjson

The SDK will take advantage of [python-rapidjson][1] for faster json processing
if it's installed.

[1]: https://pypi.python.org/pypi/python-rapidjson

### wsaccel

There are most two notable CPU intensive routines in websocket communication:
UTF-8 validation and payload masking. Fortunately there exists the
[wsaccel package][2] that provides optimized versions of said routines.

To enable the SDK to use wsaccel, use the following code:

```
import satori.rtm.connection
satori.rtm.connection.enable_wsaccel()
```

[2]: https://pypi.python.org/pypi/wsaccel

# Documentation

You can view the latest Python SDK documentation _here_.

# Development

## Development dependencies

There more build-time dependencies than runtime dependencies.
In order to work on satori-sdk-python development, you need:

 * [State Machine Compiler (SMC)][2]
    to convert state machines description into Python source code
 * [tox][3]
    to run tests using all supported Python interpreters in separate sandboxes.

[3]: http://smc.sourceforge.net/
[4]: https://tox.readthedocs.org/en/latest/

## Running Tests

Tests require an active Satori to be available. The tests require `credentials.json` 
to be populated with the Satori properties.

The `credentials.json` file must include the following key-value pairs:

```
{ 
  "endpoint": "ws://<SATORI_HOST>/",
  "appkey": "my_appkey",
  "superuser_role_secret": "ROLE SECRET KEY"
}
```
* `endpoint` is your customer-specific DNS name for Satori access.
* `appkey` is your application key.
* `superuser_role_secret` is a role secret key for a role named `superuser` that has access to the 
reserved channels. If this role does not exist, you must create it.

After setting up `credentials.json`, run SDK tests with the following commands:

```
export SMC_JAR=/path/to/Smc.jar
tox -e py27-test
```

Substitute `py27` with one of `py26`, `pypy`, `py34` or `py35` to choose a
desired Python implementation.