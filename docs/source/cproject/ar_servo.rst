.. _ar_servo:

3.7 - Swinging Servo
=======================

In this kit, in addition to LED and passive buzzer, there is also a device controlled by PWM signal, Servo.

Servo is a position (angle) servo device, which is suitable for those control systems that require constant angle changes and can be maintained. It has been widely used in high-end remote control toys, such as airplanes, submarine models, and remote control robots.

Now, try to make the servo sway!

* :ref:`cpn_servo`

**Bill of Materials**

In this project, we need the following components. 

It's definitely convenient to buy a whole kit, here's the link: 

.. list-table::
    :widths: 20 20 20
    :header-rows: 1

    *   - Name	
        - ITEMS IN THIS KIT
        - LINK
    *   - Kepler Kit	
        - 450+
        - |link_kepler_kit|

You can also buy them separately from the links below.

.. list-table::
    :widths: 5 20 5 20
    :header-rows: 1

    *   - SN
        - COMPONENT	
        - QUANTITY
        - LINK

    *   - 1
        - Raspberry Pi Pico W
        - 1
        - |link_picow_buy|
    *   - 2
        - Micro USB Cable
        - 1
        - 
    *   - 3
        - Breadboard
        - 1
        - |link_breadboard_buy|
    *   - 4
        - Wires
        - Several
        - |link_wires_buy|
    *   - 5
        - Servo
        - 1
        - |link_servo_buy|

**Schematic**

|sch_servo|

**Wiring**

|wiring_servo|

* Orange wire is signal and connected to GP15.
* Red wire is VCC and connected to VBUS(5V).
* Brown wire is GND and connected to GND.

**Code**


.. note::

   * You can open the file ``3.7_swinging_servo.ino`` under the path of ``kepler-kit-main/arduino/3.7_swinging_servo``. 
   * Or copy this code into **Arduino IDE**.


    * Don't forget to select the board(Raspberry Pi Pico) and the correct port before clicking the **Upload** button.

    

.. raw:: html
    
    <iframe src=https://create.arduino.cc/editor/sunfounder01/d52a67be-be6b-4cbf-b411-810160f56928/preview?embed style="height:510px;width:100%;margin:10px 0" frameborder=0></iframe>


When the program is running, we can see the Servo Arm swinging back and forth from 0° to 180°. 


**How it works?**

By calling the library ``Servo.h``, you can drive the servo easily. 

.. code-block:: arduino

    #include <Servo.h> 

**Library Functions：**

.. code-block:: arduino

    Servo

Create **Servo** object to control a servo.

.. code-block:: arduino

    uint8_t attach(int pin); 

Turn a pin into a servo driver. Calls pinMode. Returns 0 on failure.

.. code-block:: arduino

    void detach();

Release a pin from servo driving.

.. code-block:: arduino

    void write(int value); 

Set the angle of the servo in degrees, 0 to 180.

.. code-block:: arduino

    int read();

Return that value set with the last write().

.. code-block:: arduino

    bool attached(); 

Return 1 if the servo is currently attached.