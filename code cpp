#include <Servo.h>

// Definición de Pines
const int TRIG_PIN = 9;
const int ECHO_PIN = 8;
const int SERVO_PIN = 10;
const int LED_ROJO = 5;
const int LED_VERDE = 6;

Servo miServo;

void setup() {
  pinMode(TRIG_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  pinMode(LED_ROJO, OUTPUT);
  pinMode(LED_VERDE, OUTPUT);
  
  miServo.attach(SERVO_PIN);
  miServo.write(0); // Barrera cerrada por defecto
  
  digitalWrite(LED_ROJO, HIGH);
  digitalWrite(LED_VERDE, LOW);
  
  Serial.begin(9600);
}

void loop() {
  long duracion;
  long distancia;

  // Generar pulso ultrasónico
  digitalWrite(TRIG_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIG_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIG_PIN, LOW);

  duracion = pulseIn(ECHO_PIN, HIGH);
  distancia = duracion * 0.034 / 2;

  // Detección de vehículo (menor o igual a 15 cm)
  if (distancia > 0 && distancia <= 15) {
    digitalWrite(LED_ROJO, LOW);
    digitalWrite(LED_VERDE, HIGH);
    miServo.write(90); // Abrir barrera
    delay(3000);       // Esperar 3 segundos
  } else {
    digitalWrite(LED_ROJO, HIGH);
    digitalWrite(LED_VERDE, LOW);
    miServo.write(0);  // Cerrar barrera
  }

  delay(100);
}
