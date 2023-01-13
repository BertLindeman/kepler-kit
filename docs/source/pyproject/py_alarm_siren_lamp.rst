.. _py_alarm_lamp:

7.3 Alarm Siren Lamp
=======================

Police lights are often visible in real life (or in movies). Usually, it is used to maintain traffic, serve as a warning device, and serve as an important safety prop for officers, emergency vehicles, fire trucks, and engineering vehicles. When you see its lights or hear its sound, you must be careful, which means you (or those around you) may be in danger.

An LED and buzzer are used here to create a small warning light, which is activated by a slide switch.

|sirem_alarm|


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
        - LED
        - 1
        - |link_led_buy|
    *   - 6
        - Transistor
        - 1(S8050)
        - |link_transistor_buy|
    *   - 7
        - Resistor
        - 3(1KΩ, 220Ω, 10KΩ)
        - |link_resistor_buy|
    *   - 8
        - Passive Buzzer
        - 1
        - |link_passive_buzzer_buy|
    *   - 9
        - Capacitor
        - 1(104)
        - |link_capacitor_buy|
    *   - 10
        - Slide Switch
        - 1
        - 


**Schematic**

|sch_alarm_siren_lamp|

* GP17 is connected to the middle pin of the slider, along with a 10K resistor and a capacitor (filter) in parallel to GND, which allows the slider to output a steady high or low level when toggled to the left or right.
* As soon as GP15 is high, the NPN transistor conducts, causing the passive buzzer to start sounding. This passive buzzer is programmed to gradually increase in frequency to produce a siren sound.
* An LED is connected to GP16 and is programmed to periodically change its brightness in order to simulate a siren.



**Wiring**

|wiring_alarm_siren_lamp|


**Code**

.. note::

    * Open the ``7.3_alarm_siren_lamp.py`` file under the path of ``kepler-kit-main/micropython`` or copy this code into Thonny, then click "Run Current Script" or simply press F5 to run it.

    * Don't forget to click on the "MicroPython (Raspberry Pi Pico)" interpreter in the bottom right corner. 

    * For detailed tutorials, please refer to :ref:`open_run_code_py`.


.. code-block:: python

    import machine
    import time


    buzzer = machine.PWM(machine.Pin(15))
    led = machine.PWM(machine.Pin(16))
    led.freq(1000)

    switch = machine.Pin(17,machine.Pin.IN)

    def noTone(pin):
        pin.duty_u16(0)


    def tone(pin,frequency):
        pin.freq(frequency)
        pin.duty_u16(30000)

    def interval_mapping(x, in_min, in_max, out_min, out_max):
        return (x - in_min) * (out_max - out_min) / (in_max - in_min) + out_min

    def toggle(pin):
        global bell_flag
        bell_flag = not bell_flag
        print(bell_flag)
        if bell_flag:
            switch.irq(trigger=machine.Pin.IRQ_FALLING, handler=toggle)
        else:
            switch.irq(trigger=machine.Pin.IRQ_RISING, handler=toggle)


    bell_flag = False
    switch.irq(trigger=machine.Pin.IRQ_RISING, handler=toggle)



    while True:
        if bell_flag == True:
            for i in range(0,100,2):
                led.duty_u16(int(interval_mapping(i,0,100,0,65535)))
                tone(buzzer,int(interval_mapping(i,0,100,130,800)))
                time.sleep_ms(10)
        else:
            noTone(buzzer)
            led.duty_u16(0)

Once the program is running, toggle the slide switch to the left (yours may be to the right, depending on how your slide switch is wired) and the buzzer will emit a progressive warning tone and the LED will change its brightness accordingly; toggle the slide switch to the right and the buzzer and LED will stop working.