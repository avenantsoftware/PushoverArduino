PushoverArduino
===============

Send Pushover messages from the arduino

if you want to use for example a vaiable in the message, like a temperature reading from a temperature sensor.

Here is an example:

char Text[40];

char temp_str[8];

dtostrf(TemperatureSensor, 4, 1, temp_str); // convert float value from temperature sensor reading to a string, where TemperatureSensor is a variable defined from a temperature sensor

sprintf(Text,"The current temperature is now %s°",temp_str);

pushover(Text,0);

