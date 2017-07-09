.. image:: https://img.shields.io/:license-mit-blue.svg
    :target: http://doge.mit-license.org

.. image:: https://badge.fury.io/py/py-momit-cool-remote
    :target: https://pypi.python.org/pypi/py-momit-cool-remote

``py-momit-cool-remote`` is a Python 3 library for remotely controlling your air conditioning unit through the use of the Momit Cool.

The Momit Cool is a small device that can be attached to your AC, allowing you to control it from your smart phone. In order to accomplish remote control from anywhere, commands are sent to their central server, which then sends them to your Momit Gateway device. There are two problems with this:

1. If Momit goes bankrupt and shuts down their servers, everything will stop working.
2. It is extremely unsecure, all the traffic goes unencrypted over the wire.

``py-momit-cool-remote`` communicates directly with the Momit Gateway, completely circumventing Momit's servers.

Details
-------
I uncovered most of the information by ARP poisoning and intercepting the traffic between the Momit Gateway and the Momit servers. The Momit Gateway communicates over the CoAP protocol.

**Turning on**

.. code-block::

    PUT /10242/0/0
    Content-Format: 1541
    cm=cool,t=1335,sp=210

**Turning off**

.. code-block::

    PUT /10242/0/0
    Content-Format: 1541
    cm=cool,t=0,sp=off

Example usage
-------------

.. code-block:: python

    from momitcool import MomitCool

    cool = MomitCool('192.168.3.164')
    cool.on()
    cool.off()