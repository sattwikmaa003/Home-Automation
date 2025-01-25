# Home-Automation
#define BLYNK_PRINT Serial
#define BLYNK_TEMPLATE_ID &quot;TMPLQkEF9z57&quot;
#define BLYNK_DEVICE_NAME &quot;HOME AUTOMATION&quot;
#define BLYNK_AUTH_TOKEN &quot;qd2sCWkopxka551lN69BAp0vQgmkq-xT&quot;

#include &lt;ESP8266WiFi.h&gt;
#include &lt;BlynkSimpleEsp8266.h&gt;
char auth[] = BLYNK_AUTH_TOKEN;
char ssid[] = &quot;AriTra&quot;;
char pass[] = &quot;htcf9295&quot;;

/* HC-SR501 Motion Detector */
#define ledPin D4
#define pirPin D1 // Input for HC-S501
int pirValue; // Place to store read PIR Value

void setup()
{
Serial.begin(115200);
delay(10);
Blynk.begin(auth, ssid, pass);
pinMode(ledPin, OUTPUT);
pinMode(pirPin, INPUT);
//digitalWrite(ledPin, LOW);
}

/***************************************************
* Get PIR data
**************************************************/
void getPirValue(void)
{
pirValue = digitalRead(pirPin);
if (pirValue)
{
Serial.println(&quot;==&gt; Motion detected&quot;);
//Blynk.notify(&quot;T==&gt; Motion detected&quot;);
digitalWrite(ledPin, HIGH);
//Blynk.virtualWrite(V0,pirValue);
Blynk.virtualWrite(V1,pirValue);
}

else {
digitalWrite(ledPin, LOW); // turn LED OFF if we have no motion
//digitalWrite(buzzer, LOW); // turn LED ON
Serial.println(&quot;Hey I not got you!!!&quot;);
// Blynk.virtualWrite(V0,pirValue);
Blynk.virtualWrite(V1,pirValue);

}
}
void loop()
{
getPirValue();
Blynk.run();
}
