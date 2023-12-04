# raspberryPi-rubberduck

**Disclaimer:**
Questo progetto è stato realizzato a scopo puramente educativo e dimostrativo, per illustrare alcune tecniche e vulnerabilità informatiche. Non mi assumo alcuna responsabilità per l’uso illecito o dannoso che si potrebbe fare di queste informazioni. Chiunque utilizzi questo progetto lo fa a suo rischio e pericolo, e si assume la responsabilità di eventuali danni a cose, persone e furti di dati. Si raccomanda di usare questo progetto solo in ambienti controllati e con il consenso dei legittimi proprietari dei sistemi o delle reti da testare.

# Installazione

1.	Clonare il repository per ottenere una copia locale dei file. Cartella: git clone https://github.com/dbisu/pico-ducky.git
2.	Scarica CircuitPython per Raspberry Pi Pico.  
Scarica CircuitPython per Raspberry Pi Pico W. 
3.	Collega il dispositivo a una porta USB tenendo premuto il pulsante di avvio. Verrà visualizzato come un dispositivo multimediale rimovibile denominato RPI-RP2.
4.	Copiare il file .uf2 scaricato nella directory principale del Pico (RPI-RP2). Il dispositivo si riavvierà e dopo circa un secondo si ricollegherà come CIRCUITPY. 
5.	Scarica adafruit-circuitpython-bundle-8.x-mpy-YYYYMMDD.zip qui ed estrailo all'esterno del dispositivo.
6.	Passare a lib nella cartella estratta di recente e copiare adafruit_hid, asyncio, adafruit_wsgi, adafruit_debouncer.mpy e adafruit_ticks.mpy nella cartella lib sul Raspberry Pi Pico.
7.	Scarica circuitpython-keyboard-layouts-8.x-mpy-20221209, copia dalla cartella lib i due file: keycode_win_it e keycode_layout_win_it e incollalo nella cartella lib dela raspberry. Nel file duckyinpython controlla che sono commentate le righe per usare layout US e che sia coretto le rige per usare layout IT:
8.	
 
  #from adafruit_hid.keyboard_layout_us import KeyboardLayoutUS as KeyboardLayout
  #from adafruit_hid.keycode import Keycode
  
  from keyboard_layout_win_it import KeyboardLayout
  from keycode_win_it import Keycode

(se usi un'altra lingua come tastiera modifica i dati in base alla tua lingua)
8.	Copia boot.py, duckyinpython.py, code.py, webapp.py e wsgiserver.py dal tuo clone alla radice del tuo Pico.
  a.	Solo per Pico W Creare il file secrets.py nella radice di Pico W. Contiene il nome e la password dell'access point che devono essere creati dal Pico W.
  segreti = { 'ssid' : "NameWifi", 'password' : "Wifipassword" }
  b.	All’avvio del raspberry apparirà una nuova rete Wifi con nome NameWifi e password: Wifipassword. Apri il bowser e recati sul url: http://192.168.4.1:80 dove potrai gestire il rapsberry duck senza colleganti diretti al pc
9.	Trova uno script qui o creane uno tuo usando Ducky Script e salvalo come payload.dd nel Pico. Attualmente, pico-ducky supporta solo DuckyScript 1.0, non 3.0.
Attenzione, se il dispositivo non è in modalità di configurazione, il dispositivo si riavvierà e dopo mezzo secondo verrà eseguito lo script.
Nota: per impostazione predefinita, Pico W non verrà visualizzato come unità USB

# INFO: 
# Modalità di configurazione
Per modificare il payload, entrare in modalità di configurazione collegando il pin 1 () al pin 3 (), questo impedirà al pico-ducky di iniettare il payload nella propria macchina. Il modo più semplice per farlo è utilizzare un ponticello tra quei pin.

# Modalità di abilitazione/disabilitazione USB
Se hai bisogno che il pico-ducky non venga visualizzato come dispositivo di archiviazione di massa USB per nasconderti, segui queste istruzioni. Collegare un ponticello tra il pin 18 () e il pin 20 (). Ciò impedirà al pico-ducky di apparire come un'unità USB quando è collegato al computer di destinazione.
Pico: La modalità predefinita è l'archiviazione di massa USB abilitata.
Pico W: la modalità predefinita è la memoria di massa USB disabilitata

# Carichi utili multipli
È possibile memorizzare più carichi utili su Pico e Pico W. Per selezionare un carico utile, mettere su GND i pin seguenti:
GP4 - payload.dd
GP5 - carico utile2.dd
GP10 - carico utile3.dd
GP11 - carico utile4.dd
