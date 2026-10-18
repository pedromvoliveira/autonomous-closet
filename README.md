# autonomous-closet
A prototype of an autonomous closet 
#define DIR_PIN 7
#define STEP_PIN 6

const int STEPS_PER_REVOLUTION = 200;
const int MICROSTEPPING = 8;

const int TOTAL_STEPS = STEPS_PER_REVOLUTION * MICROSTEPPING;

void girarPassos(int passos) {

  for (int i = 0; i < passos; i++) {

    digitalWrite(STEP_PIN, HIGH);
    delayMicroseconds(800);

    digitalWrite(STEP_PIN, LOW);
    delayMicroseconds(800);
  }
}

void setup() {

  pinMode(DIR_PIN, OUTPUT);
  pinMode(STEP_PIN, OUTPUT);

  Serial.begin(9600);

  Serial.println("Digite um numero de 1 a 12");
}

void loop() {

  if (Serial.available()) {

    int numero = Serial.parseInt();

    if (numero >= 1 && numero <= 12) {

      int graus = numero * 30;

      int passos = (graus * TOTAL_STEPS) / 360;

      Serial.print("Girando ");
      Serial.print(graus);
      Serial.println(" graus");

      digitalWrite(DIR_PIN, HIGH);
      girarPassos(passos);

      delay(5000);

      Serial.println("Voltando origem");

      digitalWrite(DIR_PIN, LOW);
      girarPassos(passos);
    }
  }
}
