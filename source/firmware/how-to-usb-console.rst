###################
How to: USB Console
###################

.. warning::

    For Core Module R2 with FTDI chip please follow **How to: UART interface** tutorial and use UART2 for communication over FTDI to your computer.
    USB CDC console works only on older Core Module R1 where chip talks directly to the computer.

`Core Module <https://shop.hardwario.com/core-module/>`_ **REV 1** can handle two-way communication with USB-connected device (computer, router, ...)
over Virtual Com Port VCP.

.. tip::

    Visit `documentation for this SDK module <https://sdk.hardwario.com/group__bc__usb__cdc.html>`_

*************
Prerequisites
*************

First you have to include the USB CDC library

.. code-block:: c

    #include <bc_usb_cdc.h>

and use the library's *init* function (in your *application_init* function):

.. code-block:: c

    bc_usb_cdc_init();

************************
Sending Data to Computer
************************

To send data to your computer you have to use this function:

``bc_usb_cdc_write(const void *buffer, size_t length)``.
There are several ways to use this function probably, but the straight one is to store every data you need to send inside an array of chars,
and send this "string" over USB.

Let's say we have some text stored in the variable ``char buffer[50]`` and we want to send it to our computer.
All we have to do is to call function ``bc_usb_cdc_write(const void *buffer, size_t length)``, so in our case we call it this way:

.. code-block:: c

    bc_usb_cdc_write(buffer, strlen(buffer))

**If you need to send more type of values** (char, float and int for example) you can use the `sprintf <http://www.cplusplus.com/reference/cstdio/sprintf/>`_
function to put these values into char array.
It works like the *printf* function, but instead of sending the output to *stdout*, it stores the content inside variable.

.. tip::

    **If you can not guarantee that data will fit to pointed char buffer**
    ...you can use safer `snprintf <http://www.cplusplus.com/reference/cstdio/snprintf/>`_ function

In the example below we use internal thermometer placed on Core module to get and send some real data.
On every press of a button the application sends actual temperature and total count of "events" - when the button was pressed.
So after few presses, your computer should receive something like this:

.. code-block:: console
    :linenos:

    Temperature: 26.437500
    #3
    Temperature: 26.437500
    #4
    Temperature: 26.437500
    #5
    Temperature: 26.687500
    #6

*******
Example
*******

.. code-block:: c
    :linenos:

    #include <bcl.h>
    #include <bc_usb_cdc.h>

    bc_button_t button;
    bc_tmp112_t temp;

    float temperature = 0.0;
    int numberOfMeasurements = 0;

    void button_event_handler(bc_button_t *self, bc_button_event_t event, void *event_param)
    {
        (void) self;
        (void) event_param;

        if (event == BC_BUTTON_EVENT_PRESS)
        {
            numberOfMeasurements++;
            bc_tmp112_measure(&temp);
            bc_tmp112_get_temperature_celsius(&temp, &temperature);

            char buffer[100];

            sprintf(buffer, "Temperature: %f\r\n#%d\r\n", temperature, numberOfMeasurements);
            bc_usb_cdc_write(buffer, strlen(buffer));
        }
    }


    void application_init(void)
    {
        bc_button_init(&button, BC_GPIO_BUTTON, BC_GPIO_PULL_DOWN,0);
        bc_button_set_event_handler(&button, button_event_handler, NULL);

        bc_usb_cdc_init();

        bc_tmp112_init(&temp, BC_I2C_I2C0, 0x49);
        bc_tmp112_measure(&temp);
    }
