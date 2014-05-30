PushoverArduino
===============

Send Pushover messages from the arduino

You can use it in your own code by adding:

[code]// Pushover settings
char pushoversite[] = "api.pushover.net";
char apitoken[] = "your30characterapitokenhere123";
char userkey [] = "your30characteruserkeygoeshere";

byte pushover(char *pushovermessage, int priority)
{
  String message = pushovermessage;

  length = 93 + message.length();

  if(client.connect(pushoversite,80))
  {
    client.println("POST /1/messages.json HTTP/1.1");
    client.println("Host: api.pushover.net");
    client.println("Connection: close\r\nContent-Type: application/x-www-form-urlencoded");
    client.print("Content-Length: ");
    client.print(length);
    client.println("\r\n");;
    client.print("token=");
    client.print(apitoken);
    client.print("&user=");
    client.print(userkey);
    client.print("&message=");
    client.print(message);
    client.print("&priority=");
    client.print(priority);
    while(client.connected())  
    {
      while(client.available())
      {
        char ch = client.read();
        Serial.write(ch);
      }
    }
    client.stop();
  }  
}[/code]

and then call the function by:

pushover("whatever message",0); // 0 = default message priority, change to -2,-1,0,1,2 for different priorities

if you want to use for example a vaiable in the message, like a temperature reading from a temperture sensor.

Here is an example

char Text[40];
char temp_str[8];

dtostrf(TemperatureSensor, 4, 1, temp_str); // where TemperatureSensor is a variable defined from a temperature sensor
sprintf(Text,"The current temperature is now %s°",temp_str); // convert float value from temperature sensor reading to a string
pushover(Text,0);

