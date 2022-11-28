# SmartHome - rozwiązania typu DIY

To repozytorium zawiera kilka pomysłow na rozwiąnia DIY integrujące się z Home Assistantem, Suplą i podobnymi systemami. Być może istnieją gotowce do kupienia na zagranicznych portalach aukcyjnych za niewielkie pieniądze, jednak satysfakcji ze zrobienia czegoś samodzielnie nie da się wycenić ;-)



## Co do czego?

* eagle/ - schematy i projekty płytek zrobione w Autodesk Eagle
* esphome/ - przykładowe konfiguracje dla ESPHome wykorzystujące daną płytkę

### LD-100
Prosty sterownik LEDów RGB (są tu tylko trzy kanały, więc sterować paskiem RGBW alob RGBWW się nie da) oraz WS2818 (paski LED, gdzie da się sterować każdą diodą oddzielnie). Oparty na ESP8266. Działa po WiFi z ESPHome (banalna integracja z Home Assistantem). UWAGA: Ten sterownik jest zasilany wyłącznie na 5V, więc większość popularnych taśm LED (wymagających 12V) nie będzie z nim działać.
[TODO: Zrobić próby i określić prądy, które AO3400 wytrzymują bez chłodzenia] 

### UD-100
Prosty sterownik LEDów RGBW (cztery kanały) oparty na ESP8266 oraz tranzystorach IRLR024N. Dodatkowo, zamiast czwartego kanału na płytce znalazło się miejsce dla czujnika temperatury (DS18B20) lub podczerwieni (TSOP1736). Nominalnie zasilany z 12V, więc kompatyilny z większością popularnych tasiemek LED (mono, RGB, RGBW).



## Jak to zaprogramować?

### ESP8266, ESP32
Projekty oparte na ESP8266 i ESP32 wymagają do programowania konwertera USB-RS232. Koniecznie ustawionego na 3.3V (5V może usmażyć nasze ESP) oraz programu esptool (https://github.com/espressif/esptool). Wszystkie płytki (jeżeli w opisie nie zaznaczyłem inaczej) posiadają złącze do programowania w formacie (GND-RX-TX-RST-VCC).

W najprostszej wersji używamy tylko pierwszych trzech PINów oraz "natywnego" zasilania płytki (podczas programowania chip ESP potrzebuje sporo prądu i duża część konwerterów USB-RS232 nie daje sobie z tym rady).

W wielkim skrócie i w najprostszym przypadku podłączamy trzy pierwsze PINy (czyli GND, RX, TX), naciskamy switch podpięty do portu GPIO0, podpinamy zasilanie i ruchamiamy "esphome run jakis_plik.yaml".
