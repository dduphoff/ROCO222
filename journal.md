# LAB 2 Brushed DC motor #

A brushed DC motor works by using the current in a coil of wire. The brushes supply the armature with current and allow the current in the coil to change direction every half a rotation.  The magnets on the outside force the wire to move.
### Part 1
### Building a brushed DC motor

We first attached the pins onto the wooden base with some screws and washers to keep the pins in place. We arranged the pins in a square as can be seen fig.1.
![alt text](https://github.com/dduphoff/ROCO222/blob/master/seafc.jpg) fig. 1

For the armature we used a cork. We put 1 nail into each side. Made 2 commutators from copper wire. And spun 52 coils of enameled copper wire around it. In the end it looked like fig.2 

![alt text](https://github.com/dduphoff/ROCO222/blob/master/ertvecrtr.jpg) fig. 2



Next we mount the armature and the magnets at the end it should look like fig. 3

![alt text](https://github.com/dduphoff/ROCO222/blob/master/ertbhervht.jpg) fig. 3





We made the brushes from copper tape and mounted them under the pins to be touching the armature in front of the magnet.  Connected the non-brush end of the copper tape to a power supply. 
The final product looked like fig. 4.




![alt text](https://github.com/dduphoff/ROCO222/blob/master/rebh6bft.jpg) fig. 4


 



  






### PART 3 build a better DC motor






2nd design

we will improve the rotor to be mounted on 2 608 series bearings 
these bearings will be mounted onto a wooden base rather than paper clips 
the 608 series bearings have an inner ring diameter of 8 mm so the rotor will havto be mounted on an 8mm rod. 
the outer diameter or the bearing is 22mm

 

 

i have also deigned a bit for the magnets to be mounted on where the brushes can also be mounted on later.

the brushes will be mounted to that they face the right direction and are constantly pushed onto the rotor by some springs.

https://www.gearbest.com/skateboard/pp_322027.html?currency=GBP&vip=2684712&gclid=CjwKCAjwpfzOBRA5EiwAU0ccN2q2DFU7Fi7PKN8jcrKhMKmR-5vS0xylq82RUr5O7uctHHzuDIWhZxoCktkQAvD_BwE

19.10.17

today i changed the design for the brush mounts and the bearing holder.
they will be fitted together like a puzzle.

 
![alt text](https://github.com/dduphoff/ROCO222/blob/master/drgcv.jpg)
This piece has a rounded top and a hole in the middle (22mm diameter)  to mount an abec-9 ball bearing. these has an outer diameter of 22mm and an inner diameter of 8mm. i will have 2 of these pieces with one ball bearing in each. the wings on the side are to fit them with the brush mounts. they are 5mm x 40mm.

 
![alt text](https://github.com/dduphoff/ROCO222/blob/master/eehetyjbyu.jpg)
this is the brush/ magnet mount. it is 18cm long and 7cm high it has little locks on the aside to ensure a perfect fit with the bearing mount. holes will be drilled in it to hold the brushes.

 ![alt text](https://github.com/dduphoff/ROCO222/blob/master/hth6rv46v.jpg)
this piece is used to split up the wires and ensure they have an even distribution. it is a 60 degree wedge of a circle with a diameter smaller than that of the cork. 

 
![alt text](https://github.com/dduphoff/ROCO222/blob/master/rtvhrthcd.jpg)

the last piece. 
this is to mount on top of the wire splitters to ensure that the bar can be mounted to the rotor.
it has the same diameter as the cork (19.05mm) and an inner diameter same as the abec-9 ball bearings. this allows me to slide an 8mm bar into both ends of the rotor and attach them to the ball bearings.

for the brushes i will use some wooden bits layered in copper tape. they will be held onto the contacts with little weights. 


# Lab 3 build an incremental encoder 

An incremental encoder is made up of a IR photosensor and an infrared LED. An encoder disk is attached to the motor. Every time the disk leaves space the circuit detects light passing through the disk. Knowing how the disk is laid out the rate of rotation of the motor can be measured and even controlled.

To wire up the circuit we need an infrared LED, a infrared photodetector, 10k and 100k resistors, a supply wire a ground wire and a signal wire. The LED and transistor must be facing each other with enough space for the disk to comfortably fit in-between the two.



We are going to be using a disk with one wedge cut out of it. This means that every time the IR light is detected we can count one rotation. It is going to be cut out of cardboard and mounted onto the motor using glue tack.




We mounted the motor to the desk and held the incremental encoder so that it would detect the wedge cut out from the encoder disk. 


![alt text](https://github.com/dduphoff/ROCO222/blob/master/24726887_10214949324391123_1632369383_n.jpg)




##### The code I used to calculate rate of rotation was:
const byte ledPin = 13;
const byte interruptPin = 2;
volatile byte state = LOW;
int count = 0;
int ang_v ;
void setup() {
pinMode(ledPin, OUTPUT);
pinMode(interruptPin, INPUT);
// configure the interrupt call-back: blink is called everytime the pin
// goes from low to high.
attachInterrupt(digitalPinToInterrupt(interruptPin), blink, RISING);
Serial.begin(9600);

}



void loop() {
delay(1000)  ;
Serial.println(count);
count = 0;
}
void blink() {

count += 1;
}


The maximum result after 20 seconds of running the motor the maximum rate of rotation was 293rps at 1.5V . 


# LAB 4 Controlling the motor: #

Unfortunately my motor design was too heavy to work 



Instead I used the Arduino to control the speed of a 3v dc motor I coded it so that the serial monitor would print the number of rotations every second. 


##### using this code: ##
const byte ledPin = 13;
const byte interruptPin = 2;
volatile byte state = LOW;
int count = 0;
int r = 50 ; //desired rotations
int rcount ;
void setup() {
pinMode(ledPin, OUTPUT);
pinMode(interruptPin, INPUT);
// configure the interrupt call-back: blink is called everytime the pin
// goes from low to high.
attachInterrupt(digitalPinToInterrupt(interruptPin), blink, RISING);
Serial.begin(9600);


}



void loop() {
delay(1000)  ;
analogWrite(9 , r);

rcount = Serial.println(count);
count = 0;
if (rcount > r) 
r += 1 ;

else if (rcount < r)
 r -=1 ; 

else 


}
void blink() {

count += 1;
}

# LAB 5 stepper motors

Stepper motors work using at least 2 pairs or coils that are alternatively activated to move the rotor. They come in unipolar and bipolar mode. In unipolar mode the motor requires 5-6 wires since they all share a common ground. In bipolar mode it works with 4 wires that the Arduino can control via an H-Bridge  .They work in 4 different modes. Full step mode, double step mode, half step mode and micro stepping mode. Stepper motors are more durable compared to brushed dc motors mostly because the brushes are the most vulnerable part of the motor. 



I wired it up using 4 cables 









#### Code (full step half step and double step) :
##### Full step:





void setup() {
  
  //establish motor direction toggle pins
  pinMode(12, OUTPUT); //CH A -- HIGH = forwards and LOW = backwards???
  pinMode(13, OUTPUT); //CH B -- HIGH = forwards and LOW = backwards???
  
  //establish motor brake pins
  pinMode(9, OUTPUT); //brake (disable) CH A
  pinMode(8, OUTPUT); //brake (disable) CH B


  
  
}

void loop(){
 
  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, HIGH); //engage break  B

  digitalWrite(12, HIGH);   //DIR A
  analogWrite(3, 255);   //PWM A
  
  delay(100);
  
  digitalWrite(9, HIGH);  //engage break A
  digitalWrite(8, LOW); //disengage break B

  digitalWrite(13, LOW);   //DIR B
  analogWrite(11, 255);   //PWM B
  
  delay(100);
  
  digitalWrite(9, LOW);  //disengage break A
  digitalWrite(8, HIGH); //engage break B

  digitalWrite(12, LOW);   //DIR A
  analogWrite(3, 255);   //PWM A
  
  delay(100);
    
  digitalWrite(9, HIGH);  //engage break A
  digitalWrite(8, LOW); //disengage break B

  digitalWrite(13, HIGH);   //DIR B
  analogWrite(11, 255);   //PWM B
  
  delay(100);

}


##### Double step:





void setup() {
  
  //establish motor direction toggle pins
  pinMode(12, OUTPUT); //CH A -- HIGH = forwards and LOW = backwards???
  pinMode(13, OUTPUT); //CH B -- HIGH = forwards and LOW = backwards???
  
  //establish motor brake pins
  pinMode(9, OUTPUT); //brake (disable) CH A
  pinMode(8, OUTPUT); //brake (disable) CH B


  
  
}

void loop(){
 
  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, LOW); //engage break  B
  digitalWrite(12, HIGH);   //DIR A
  digitalWrite(13, HIGH);   //DIR A

  
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM B
  
  

  delay(100);
  
  digitalWrite(12, LOW);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM B
  
  delay(100);

  
digitalWrite(13, LOW);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM B


  delay(100);
  
  digitalWrite(12, HIGH);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM B

   delay(100);
  
  

}


##### Half step:





void setup() {
  
  //establish motor direction toggle pins
  pinMode(12, OUTPUT); 
  pinMode(13, OUTPUT); 
  
  //establish motor brake pins
  pinMode(9, OUTPUT); 
  pinMode(8, OUTPUT); 


  
  
}

void loop(){
 
  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, HIGH); //engage break  B

  digitalWrite(12, HIGH);   //DIR A
  analogWrite(3, 255);   //PWM A
  
  delay(100);


  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, LOW); //engage break  B

  digitalWrite(13, HIGH);   //DIR A
  digitalWrite(12, HIGH);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM A
  
  delay(100);
  
  digitalWrite(9, HIGH);  //engage break A
  digitalWrite(8, LOW); //disengage break B

  digitalWrite(13, HIGH);   //DIR B
  analogWrite(11, 255);   //PWM B
  
  delay(100);

  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, LOW); //engage break  B

  digitalWrite(13, HIGH);   //DIR B
  digitalWrite(12, LOW);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM A
  
  delay(100);

  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, HIGH); //engage break  B

  digitalWrite(12, LOW);   //DIR A
  analogWrite(3, 255);   //PWM A
  
  delay(100);

  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, LOW); //engage break  B

  digitalWrite(13, LOW);   //DIR A
  digitalWrite(12, LOW);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM A


  delay(100);

  digitalWrite(9, HIGH);  //engage break A
  digitalWrite(8, LOW); //disengage break B

  digitalWrite(13, LOW);   //DIR B
  analogWrite(11, 255);   //PWM B
  
  delay(100);

  digitalWrite(9, LOW);  //disengage break  A
  digitalWrite(8, LOW); //engage break  B

  digitalWrite(13, LOW);   //DIR B
  digitalWrite(12, HIGH);   //DIR A
  analogWrite(3, 255);   //PWM A
  analogWrite(11, 255);   //PWM B


  delay(100);
  
  

}



When testing the torque of the motor with my fingers it was clear that in full step mode the torque was the lowest and highest in 2 phase full step mode. 


### Servo motors ### 

Made a makeshift arm out of cardboard and mounted the servos. Wired it up to a potentiometer and used the knob function to control the servo. 
![alt text](https://github.com/dduphoff/ROCO222/blob/master/24891524_10214965895645394_2138005197_n.jpg)

##### I then wrote a code that used 2 potentiometers and 2 servos :

#include <Servo.h>

Servo myservo1;  // create servo object to control a servo
Servo myservo2;
int potpin1 = 0;  // analog pin used to connect the potentiometer
int potpin2 = 1;
int val1;    // variable to read the value from the analog pin
int val2; 
void setup() {
  myservo1.attach(9);  // attaches the servo on pin 9 to the servo object
  myservo2.attach(10);
}

void loop() {
  val1 = analogRead(potpin1);            // reads the value of the potentiometer (value between 0 and 1023)
  val1 = map(val1, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
  myservo1.write(val1);                  // sets the servo position according to the scaled value
  val2 = analogRead(potpin2);            // reads the value of the potentiometer (value between 0 and 1023)
  val2 = map(val2, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
  myservo2.write(val2);                  // sets the servo position according to the scaled value
  delay(15);                           // waits for the servo to get there
}
  


i then went into solidworks to get some designing done for a better robot arm with 2 degrees of freedom
it looked like this:

![alt text](https://github.com/dduphoff/ROCO222/blob/master/nmib.jpg)

when i assembled my arm it looked like this


https://youtu.be/T8CKWnWQNMo