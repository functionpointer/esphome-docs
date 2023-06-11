PPPoS Component
===============

.. seo::
    :description: Instructions for setting up the Point-to-Point Protocol over Serial configuration in ESPHome.
    :keywords: PPPoS, wired, network

This ESPHome component enables *wired* network communications over UART, using the Point-to-Point Protocol over Serial (PPPoS).

The PPPoS component is supported on RP2040.

This component, the Wi-Fi component and the Ethernet component may **not** be used simultaneously, even if multiple are physically available.

.. code-block:: yaml

  rp2040:
    board: rpipicow
    framework:
      platform_version: https://github.com/maxgerhardt/platform-raspberrypi.git
      source: https://github.com/earlephilhower/arduino-pico/releases/download/3.1.1/rp2040-3.1.1.zip
      version: 3.1.1

  uart:
    - id: uart_ppp
      tx_pin: GPIO4
      rx_pin: GPIO5
      baud_rate: 115200

  pppos:
    id: ppp0
    uart_id: uart_pppp


Configuration variables:
------------------------

- **uart_type** (*Optional*, string): Which type of UART to use.

  Supported types are:

  - ``UART_COMPONENT`` (the default)
  - USB_CDC

- **uart_id** (*Optional*, :ref:`config-id`): The ID of the :ref:`UART Component <uart>` to use. Only relevant when using ``UART_COMPONENT``.
- **id** (*Optional*, :ref:`config-id`): Manually specify the ID used for code generation.


Configuration examples
----------------------

**PPPoS over USB on Raspberry Pi Pico**:

This config works both on the Pico and on the Pico W.

.. code-block:: yaml

  rp2040:
    board: rpipicow
    framework:
      platform_version: https://github.com/maxgerhardt/platform-raspberrypi.git
      source: https://github.com/earlephilhower/arduino-pico/releases/download/3.1.1/rp2040-3.1.1.zip
      version: 3.1.1

  pppos:
    id: ppp0
    uart_type: USB_CDC

The other endpoint
------------------

The ESPHome devices becomes a client, periodically attempting to connect.
The other end of the connection is expected to supply an IPv4-Address and a DNS-Server.

On Debian (and derivatives like Raspbian) this can be accomplished like this:

.. code-block:: bash

  ~# apt install ppp
  ~# sysctl net.ipv4.ip_forward=1
  ~# pppd /dev/ttyUSB0 115200 lock nodetach noauth debug nocrtscts 10.10.8.1:10.10.8.2


This creates a new network interface with the IP-Address ``10.10.8.1``, and gives the ESPHome device the Address ``10.10.8.2``.
It also enables routing, allowing the ESPHome device to reach other devices in your network.

To make the responses reach the ESPHome device, you also need to add a static route to your home's router, pointing ``10.10.8.0/24`` to your Linux machine.

Another alternative is Network Address Translation (NAT), which can be activated using the ``MASQUERADE`` feature.

See Also
--------

- :doc:`network`
- :apiref:`pppos/pppos_component.h`
- :ghedit:`Edit`
