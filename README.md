PushoverArduino
===============

Send pushover.net messages from the arduino to your android or iOS device.

If you want to use for example a variable in the message, like a temperature reading from a temperature sensor.

Here is an example:

<pre>Text[40];

char temp_str[8];

dtostrf(TemperatureSensor, 4, 1, temp_str); // convert float value from temperature sensor reading to a string, where TemperatureSensor is a variable defined from a temperature sensor value

sprintf(Text,"The current temperature is now %s°",temp_str);

pushover(Text,0);</pre>

