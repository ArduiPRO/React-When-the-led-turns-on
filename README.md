# React-When-the-led-turns-on
    int BUT = 2 ; // determine BUT to a port 
    int LED = 9 ; // determine LED to a port
    int BUT2 = 4 ; // determine BUT2 to a port 
    int LED2 = 10; // Determine LED2 to a port 
    int BUT3 = 7;
    int LED3 = 11;
    int BUT4 = 12;
    int LED4 = 5;
    int LEDG = 8;
    int LEDY = 6;
    int LEDR = 3;
    int finalScore = 0;//define finale score 
    int maxim = 0;//define maximum score 
    int  r;//=random(4); //random value [0,4)
    int c = 0; //define correct anwsers
    int guard = 0;//define an observant to activate random  
    int buttonState = 0;//define the state of the BUT
    int buttonState2 = 0;
    int buttonState3 = 0;
    int buttonState4 = 0;
    unsigned long t;
    int Q = 15000;// define the time of the game 
    int inc = 0;//define the wrong anwsers 
    int media;//define an average 
    void setup() {
      Serial.begin(9600);

      pinMode(LED, OUTPUT); //led creats outputs
      pinMode(LED2, OUTPUT); //led2 creats outputs
      pinMode(LED3, OUTPUT); //led3 creats outputs
      pinMode(LED4, OUTPUT); //led4 creats outputs
      pinMode(BUT, INPUT); //boton creats inputs
      pinMode(BUT2, INPUT); //boton2 creats inputs
      pinMode(BUT3, INPUT); //boton3 creats inputs
      pinMode(BUT4, INPUT); //boton4 creats inputs
      pinMode(LEDG, OUTPUT);
      pinMode(LEDY, OUTPUT);
      pinMode(LEDR, OUTPUT);
      randomSeed(analogRead(0)); 

      Serial.println("Starting...");//appears on screen
      digitalWrite(LEDG, HIGH);//turn on the led 
      digitalWrite(LEDY, HIGH);
      digitalWrite(LEDR, HIGH);
      delay(1000);// 1 second delay
      Serial.println(1);
      digitalWrite(LEDG, LOW);//turn off the led 
      digitalWrite(LEDY, HIGH);
      digitalWrite(LEDR, HIGH);
      delay(1000);
      Serial.println(2);
      digitalWrite(LEDG, LOW);
      digitalWrite(LEDY, LOW);
      digitalWrite(LEDR, HIGH);
      delay(1000);
      Serial.println(3);
      digitalWrite(LEDG, LOW);
      digitalWrite(LEDY, LOW);
      digitalWrite(LEDR, LOW);
      delay(1000);
      Serial.println(4);
      digitalWrite(LEDG, HIGH);
      digitalWrite(LEDY, HIGH);
      digitalWrite(LEDR, HIGH);
      Serial.println(5);
      Serial.println("Go!");

      t = millis();// Arduino starts counting the time 

    }

    void loop() {

      if (millis() - t >= Q / 3) { //(Q/3)){// Calculates a third of the time passed 
        digitalWrite(LEDG, LOW);//turns off the green led 
      }
      if (millis() - t >= ((2 * Q) / 3)) {//Calculates two thirds of the time passed 
        digitalWrite(LEDY, LOW);//turns off the yellow led 
      }
      if (millis() - t >= Q) {//times over 
        digitalWrite(LEDR, LOW);//turns off the red led
      }
      buttonState = digitalRead(BUT);//assigns to the buttonState the state of BUT
      buttonState2 = digitalRead(BUT2);
      buttonState3 = digitalRead(BUT3);
      buttonState4 = digitalRead(BUT4);

      if (r == 0) {                     //if random 0, led1 ON and led2,3,4 OFF
        digitalWrite(LED, HIGH);
        digitalWrite(LED2, LOW);
        digitalWrite(LED3, LOW);
        digitalWrite(LED4, LOW);
        if (buttonState == LOW) { //if BUT is pressed c increases by 1, puts onther random value and turns back the state of BUT to high
          c++;
          guard = 1;
          while (digitalRead(BUT) == LOW) {//so that c doesnt increase while BUT is pressed 
          }
        } else {
          if (buttonState2 == LOW || buttonState3 == LOW || buttonState4 == LOW) {//if not inc increaes by 1 
            inc++;
          }
    while (digitalRead(BUT2) == LOW || digitalRead(BUT3) == LOW || digitalRead(BUT4) == LOW) {//so that inc doesnt increase while BUT2,3 and 4 are pressed 
          }
        }
      }
      if (r == 1) {                      //if random 1, led1,3,4 OFF and led2 ON
        digitalWrite(LED, LOW);
        digitalWrite(LED2, HIGH);
        digitalWrite(LED3, LOW);
        digitalWrite(LED4, LOW);

      if (buttonState2 == LOW) { //if BUT2is pressed c inceases by 1, puts another random value and turns back the state of BUT2 to high
          c++;
          c++;
          guard = 1;
          while (digitalRead(BUT2) == LOW) {
          }
        } else {
          if (buttonState == LOW || buttonState3 == LOW || buttonState4 == LOW) {
            inc++;
          }
          while (digitalRead(BUT) == LOW || digitalRead(BUT3) == LOW || digitalRead(BUT4) == LOW) {
          }
        }
      }

      if (r == 2) {                      //if random 2, led1,2,4 OFF and led2 ON
        digitalWrite(LED, LOW);
        digitalWrite(LED2, LOW);
        digitalWrite(LED3, HIGH);
        digitalWrite(LED4, LOW);

     if (buttonState3 == LOW) { //if BUT3 is pressed c inceases by 1, puts another random value and turns back the state of BUT3 to high
          c++;
          guard = 1;
          while (digitalRead(BUT3) == LOW) {
          }
        } else {
          if (buttonState2 == LOW || buttonState == LOW || buttonState4 == LOW) {
            inc++;
          }
          while (digitalRead(BUT) == LOW || digitalRead(BUT2) == LOW || digitalRead(BUT4) == LOW) {
          }
        }
      }

      if (r == 3) {                      //if random 3, led1,2,3 OFF and led4 ON
        digitalWrite(LED, LOW);
        digitalWrite(LED2, LOW);
        digitalWrite(LED3, LOW);
        digitalWrite(LED4, HIGH);

     if (buttonState4 == LOW) { //if BUT4 is pressed c inceases by 1, puts another random value and turns back the state of BUT4 to high
          c++;
          guard = 1;
          while (digitalRead(BUT4) == LOW) {
          }
        } else {
          if (buttonState2 == LOW || buttonState3 == LOW || buttonState == LOW) {
            inc++;
            while (digitalRead(BUT) == LOW || digitalRead(BUT2) == LOW || digitalRead(BUT3) == LOW) {
            }
          }
        }
      }

      if (guard == 1) {/restarts the random value 
        r = random(4);
        guard = 0;
      }


      if (millis() - t <= Q) {//time appears on screen from 0 to 15 
        Serial.print((millis() - t) / 1000);

        Serial.print("   ");
        Serial.print(c);//c appears on screen
        Serial.print("    ");
        Serial.println(inc);//inc appears on screen
      } else {
        Serial.println("    ");
        Serial.println("TIME OUT");
        Serial.print("CORRECT    ");
        Serial.print(c);
        Serial.println();
        Serial.print("INCORRECT   ");
        Serial.print(inc);
        Serial.println();
        Serial.print("AVERAGE    ");
        media = ((c * 100) / (c + inc));// an average appears on screen
        Serial.println(media);
        Serial.print("FINAL SCORE     ");
        finalScore = c * 100 / media;//a final score appears on screnn 
        Serial.println(finalScore);
        if (maxim < finalScore) {// if the maxium score is lower than high score maximum appears on screen
          maxim = finalScore;
        }
        Serial.print("HIGH SCORE      ");
        Serial.println(maxim);

    //restart the game 
        while (digitalRead(BUT) == HIGH || digitalRead(BUT2) == HIGH || digitalRead(BUT3) == HIGH || digitalRead(BUT4) == HIGH) {
        }
        Serial.println();
        Serial.println("Starting...");
        digitalWrite(LEDG, HIGH);
        digitalWrite(LEDY, HIGH);
        digitalWrite(LEDR, HIGH);
        delay(1000);
        Serial.println(1);
        digitalWrite(LEDG, LOW);
        digitalWrite(LEDY, HIGH);
        digitalWrite(LEDR, HIGH);
        delay(1000);
        Serial.println(2);
        digitalWrite(LEDG, LOW);
        digitalWrite(LEDY, LOW);
        digitalWrite(LEDR, HIGH);
        delay(1000);
        Serial.println(3);
        digitalWrite(LEDG, LOW);
        digitalWrite(LEDY, LOW);
        digitalWrite(LEDR, LOW);
        delay(1000);
        Serial.println(4);
        digitalWrite(LEDG, HIGH);
        digitalWrite(LEDY, HIGH);
        digitalWrite(LEDR, HIGH);
        Serial.println(5);
        Serial.println("Go!");


        t = millis();
        c = 0;
        inc = 0;
      }
    }
