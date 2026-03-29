#include <Servo.h>
#include <SoftwareSerial.h>

SoftwareSerial BT(10, 11); // RX, TX

Servo motorIleri;
Servo motorGeri;
Servo kolYukari;
Servo kolSag;
Servo kanca;

void setup() {
  Serial.begin(9600);
  BT.begin(9600);

  motorIleri.attach(3);  // örnek pinler
  motorGeri.attach(5);
  kolYukari.attach(6);
  kolSag.attach(9);
  kanca.attach(8);
}

void loop() {
  if (BT.available()) {
    char komut = BT.read();
    Serial.println(komut); // izleme için

    switch (komut) {
      case 'F':
        motorIleri.write(180); // ileri
        delay(300);
        motorIleri.write(90);  // dur
        break;

      case 'B':
        motorGeri.write(0); // geri
        delay(300);
        motorGeri.write(90);  // dur
        break;

      case 'R':
        motorIleri.write(180);
        motorGeri.write(90);
        delay(300);
        motorIleri.write(90);
        break;

      case 'L':
        motorGeri.write(0);
        motorIleri.write(90);
        delay(300);
        motorGeri.write(90);
        break;

      case 'U':
        kolYukari.write(180); delay(300); kolYukari.write(90); break;

      case 'D':
        kolYukari.write(0); delay(300); kolYukari.write(90); break;

      case 'K':
        kolSag.write(180); delay(300); kolSag.write(90); break;

      case 'H':
        kolSag.write(0); delay(300); kolSag.write(90); break;

      case 'O':
        kanca.write(180); break; // aç
      case 'C':
        kanca.write(0); break;   // kapat
    }
  }
}
