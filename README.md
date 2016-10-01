int sol_ileri = 2;//sol motorun çalışmasını tanımladım
int sol_geri = 3;

int sag_ileri = 4;//sağ motorun çalışmasını tanımladım
int sag_geri = 5;

char veri;//if kodu için veri değişkenini tanımladım

const int trigger_pin = 6; // burada mesafe sensörü tanımlandı
const int echo_pin = 7;

float sure;
float mesafe;

int mesafe_durumu = 30;

#include <Servo.h>
Servo sg90;

void setup (){
    
    pinMode(sol_ileri, OUTPUT);
    pinMode(sol_geri, OUTPUT);
    pinMode(sag_ileri, OUTPUT);
    pinMode(sag_geri, OUTPUT);
    Serial.begin(9600);
//aşşağıda gene mesafesensörü var
    pinMode(trigger_pin, OUTPUT);
    pinMode(echo_pin, INPUT);


    Serial.begin(9600);
sg90.attach(9);
sg90.write(12);

}
void loop(){ 


//BLUETOOTH-----------------
 if (Serial.available()>0){
 veri=Serial.read();
//BLUETOOTH-----------------

//MESAFE---------------------------
 digitalWrite(trigger_pin, HIGH) ;
 delayMicroseconds(1000)         ;
 digitalWrite(trigger_pin, LOW)  ;
 sure = pulseIn(echo_pin, HIGH)  ;
 mesafe = (sure/2) / 29.5;
 Serial.println(mesafe);
 mesafe = mesafe_durumu;
//MESAFE---------------------------


//ENGEL ALGILAMA
  
  if(mesafe <= mesafe_durumu){

      digitalWrite(sol_ileri, LOW); 
      digitalWrite(sag_ileri, LOW); 
    
  }
  
//ENGEL ALGILAMA


    if(veri == '1'){                                   //İLERİ BUTONUNA BASILDIĞI TAKTİRDE



        Serial.println("Robot İleri Gidiyor");
        sg90.write(12);
        digitalWrite(sol_ileri, HIGH); 
        digitalWrite(sag_ileri, HIGH);        



                  }

    

    else if(veri == 'q'){ 
        digitalWrite(sol_ileri,LOW);
        digitalWrite(sol_geri, LOW);
        digitalWrite(sag_ileri,LOW);
        digitalWrite(sag_geri, LOW);   
        sg90.write(12);

    }
        
    else if(veri == '2'){  //Robotun sağa gitmesini tanımladım
        digitalWrite(sol_ileri, LOW);
        digitalWrite(sol_geri, HIGH);
        digitalWrite(sag_ileri, HIGH);
        digitalWrite(sag_geri, LOW);
        Serial.println("Robot Sola Döndü");
                        }
         if(veri == 'w'){ 
        digitalWrite(sol_ileri,LOW);
        digitalWrite(sol_geri, LOW);
        digitalWrite(sag_ileri,LOW);
        digitalWrite(sag_geri, LOW);   
                        } 
    
    else if (veri == '3'){  //Robotun sağa dönmesini tanımladım
       digitalWrite(sol_ileri, HIGH);
        digitalWrite(sol_geri, LOW);
        digitalWrite(sag_ileri, LOW);
        digitalWrite(sag_geri, HIGH);
        Serial.println("Robot Sağa Döndü");
                         }   
 
       else if(veri == 'e'){ 
        digitalWrite(sol_ileri,LOW);
        digitalWrite(sol_geri, LOW);
        digitalWrite(sag_ileri,LOW);
        digitalWrite(sag_geri, LOW);   
                           }


    
   else if (veri == '4'){//Robot geri gidecek        
        digitalWrite(sol_ileri, LOW);
        digitalWrite(sol_geri, HIGH);
        digitalWrite(sag_ileri, LOW);
        digitalWrite(sag_geri, HIGH);
        Serial.println("Robot Geri Gidiyor");  
        sg90.write(180);

      

}   
     else if(veri == 'r'){ 
        digitalWrite(sol_ileri,LOW);
        digitalWrite(sol_geri, LOW);
        digitalWrite(sag_ileri,LOW);
        digitalWrite(sag_geri, LOW);   
        sg90.write(180);
    }

    }}
