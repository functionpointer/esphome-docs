Hydreon Rain Sensor Restart Button
=================================

.. seo::
    :description: Instructions for setting up Hydreon rain sensors
    :image: hydreon_rg9.jpg
    :keywords: hydreon

The ``hydreon_rgxx`` button platform allows you restart a Hydreon Rain Sensor whenever you want.

.. code-block:: yaml

    uart:
      rx_pin: GPIO16
      tx_pin: GPIO17
      baud_rate: 9600

    sensor:
      - platform: hydreon_rgxx
        model: "RG_9"
        id: "hydreon_1"
        moisture:
          name: "rain"
          expire_after: 30s 
		
		button:
			- platform: hydreon_rgxx
			  hydreon_rgxx_id: "hydreon_1"
			  name: "Rain sensor restart"

Configuration variables:
------------------------

- **name** (**Required**, string): The name for the button.
- **hydreon_rgxx_id** (*Optional*, :ref:`config-id`): The ID of the Hydreon Rain Sensor.
- **id** (*Optional*, :ref:`config-id`): Manually specify the ID used for code generation.
- All other options from :ref:`Button <config-button>`.

See Also
--------

- :doc:`/components/sensor/hydreon_rgxx`
- :doc:`index`
- :ghedit:`Edit`
