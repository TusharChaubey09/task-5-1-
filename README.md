# task-5-1-
const byte  upButtonPin = 2;
const byte  downButtonPin = 3;
int setpoint = 0;
bool setpointChanged = false;

void setup()
{
   
   pinMode(upButtonPin, INPUT_PULLUP);
   pinMode(downButtonPin, INPUT_PULLUP);

   Serial.begin(9600);
   Serial.println("setpoint change with 2 buttons example\n\n");
}


void loop()
{
   checkUpButton();
   checkDownButton();
   if (setpointChanged == true)
   {
      Serial.print("new setpoint = ");
      Serial.println(setpoint);
      setpointChanged = false;
   }
}

void checkUpButton()
{
   boolean buttonState = 0;        
   static boolean lastButtonState = 0;    
   static unsigned long timer = 0;
   unsigned long interval = 50; 
   if (millis() - timer >= interval)
   {
      timer = millis();

    
      buttonState = digitalRead(upButtonPin); 

   
      if (buttonState != lastButtonState)
      {
         
         if (buttonState == LOW)
         {
            
            setpoint++;
            setpointChanged = true;
         }
         
         lastButtonState = buttonState;
      }
   }
}

void checkDownButton()
{
   boolean buttonState = 0;        
   static boolean lastButtonState = 0;     
   static unsigned long timer = 0;
   unsigned long interval = 50;  
   if (millis() - timer >= interval)
   {
      timer = millis();

   
      buttonState = digitalRead(downButtonPin);

   
      if (buttonState != lastButtonState)
      {
        
         if (buttonState == LOW)
         {
           
            setpoint--;
            setpointChanged = true;
         }
        
         lastButtonState = buttonState;
      }
   }
}
