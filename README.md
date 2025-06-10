#include <Servo.h>

int adelante = 2;
int atras = 3;
char blue;
Servo direccion;
int anguloDireccion = 90; // Estado actual del servo

void setup() {
  Serial.begin(9600);

  pinMode(adelante, OUTPUT);
  pinMode(atras, OUTPUT);

  direccion.attach(9); // Cambiar este pin si es necesario
  direccion.write(90);
}

void loop() {
  if (Serial.available() > 0) {
    blue = Serial.read();

    if (blue == 'L') { // Solo gira a la izquierda
      anguloDireccion = 10;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, LOW);
      digitalWrite(atras, LOW);
    }

    if (blue == 'R') { // Solo gira a la derecha
      anguloDireccion = 145;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, LOW);
      digitalWrite(atras, LOW);
    }

    if (blue == 'F') { // Solo avanza si la dirección está recta
      if (anguloDireccion == 90) {
        digitalWrite(adelante, HIGH);
        digitalWrite(atras, LOW);
      } else {
        digitalWrite(adelante, LOW);
        digitalWrite(atras, LOW);
      }
    }

    if (blue == 'B') { // Solo retrocede si la dirección está recta
      if (anguloDireccion == 90) {
        digitalWrite(adelante, LOW);
        digitalWrite(atras, HIGH);
      } else {
        digitalWrite(adelante, LOW);
        digitalWrite(atras, LOW);
      }
    }

    if (blue == 'G') { // Avanza a la izquierda
      anguloDireccion = 10;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, HIGH);
      digitalWrite(atras, LOW);
    }

    if (blue == 'I') { // Avanza a la derecha
      anguloDireccion = 145;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, HIGH);
      digitalWrite(atras, LOW);
    }

    if (blue == 'H') { // Retrocede a la izquierda
      anguloDireccion = 10;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, LOW);
      digitalWrite(atras, HIGH);
    }

    if (blue == 'J') { // Retrocede a la derecha
      anguloDireccion = 145;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, LOW);
      digitalWrite(atras, HIGH);
    }

    if (blue == 'S') { // Detener todo
      anguloDireccion = 90;
      direccion.write(anguloDireccion);
      digitalWrite(adelante, LOW);
      digitalWrite(atras, LOW);
    }
  }
}
