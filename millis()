int led1 = 6;        // первый светодиод
int led2 = 7;        // второй светодиод
int toggleLed = 5;   // светодиод, состояние которого будет управляться с помощью нажатия кнопки. Подключен к контакту 5
int pushButton = 2;  // кнопка подключена к контакту 2, который в нашем проекте также служит контактом, на котором производится обработка прерывания
int ledState1 = LOW; // переменные для управления состоянием 1-го и 2-го светодиодов
int ledState2 = LOW;
unsigned long previousMillis1 = 0; // переменная для хранения момента времени, в который последний раз производилось переключение состояния 1-го светодиода
const long period1 = 1000;         // период в мс, с которым должен мигать 1-й светодиод
unsigned long previousMillis2 = 0; // переменная для хранения момента времени, в который последний раз производилось переключение состояния 2-го светодиода
const long period2 = 200;          // период в мс, с которым должен мигать 2-й светодиод
int debouncePeriod = 20;           // задержка для устранения дребезга контактов
int debounceMillis = 0;            // похоже на previousMillis
bool buttonPushed = false;         // состояние кнопки прерывания работы
int ledChange = LOW;      // переменная для отслеживания последнего состояния 3-го светодиода  
int lastState = HIGH;     // переменная для хранения последнего состояния кнопки

void setup() 
{
  // определим пины как входные или выходные параметры
  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(toggleLed, OUTPUT);
  pinMode(pushButton, INPUT);
  attachInterrupt(digitalPinToInterrupt(pushButton), pushButton_ISR, CHANGE); // обработка прерывания будет производиться на контакте 2 
}

void pushButton_ISR()
{
  buttonPushed = true; // функция обработки прерывания должна быть по возможности максимально короткой
}

void loop() 
{
  unsigned long currentMillis = millis(); // сохраняем текущее время
  if (currentMillis - previousMillis1 >= period1) 
  { // проверяем, прошло ли 1000 мс
    previousMillis1 = currentMillis; // сохраняем последнее время, когда мигнул светодиод
    if (ledState1 == LOW) 
    {  // если светодиод выключен, включаем его, и наоборот
      ledState1 = HIGH; // изменяем состояние светодиода для следующей итерации
    } 
    else 
    {
      ledState1 = LOW;
    }
    digitalWrite(led1, ledState1); // устанавливаем 1-й светодиод в состояние, определяемое переменной  ledState1 
  }
  
  if (currentMillis - previousMillis2 >= period2) 
  { // проверяем, прошло ли 200 мс
    previousMillis2 = currentMillis; // сохраняем последнее время, когда мигнул светодиод
    if (ledState2 == LOW) 
    { // если светодиод выключен, включаем его, и наоборот
      ledState2 = HIGH;
    } 
    else 
    {
      ledState2 = LOW;
    }
    digitalWrite(led2, ledState2); // устанавливаем 2-й светодиод в состояние, определяемое переменной ledState2
  }
  
  if (buttonPushed = true) // проверяем, вызывалась ли функция обработки прерывания (ISR) 
  {
    if ((currentMillis - debounceMillis) > debouncePeriod && buttonPushed) // организация задержки в 20 мс для устранения эффекта дребезга контактов
    {
      debounceMillis = currentMillis; // сохраняем последнее время задержки отмены
      if (digitalRead(pushButton) == LOW && lastState == HIGH) // изменяем состояние светодиода если кнопка была нажата
      {
        ledChange = ! ledChange;
        digitalWrite(toggleLed, ledChange);  
        lastState = LOW;
      }
      else if (digitalRead(pushButton) == HIGH && lastState == LOW)     
      {
        lastState = HIGH;
      }
      buttonPushed = false;
    }
  }
}
