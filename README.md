// DHT кітапханасын қосу
 #include "DHT.h" 
 // DHT сенсорының түрі
 #define DHTTYPE DHT11

// DHT11 модулінің деректерді енгізу қосылымына хабарласыңыз 
 int pinDHT11=9; 
 // топырақ ылғалдылығы модулінің аналогтық шығысын қосу контактісі
 int pinSoilMoisture=A0; 
 // TMP36 температура сенсорының аналогтық шығыс қосылымының түйреуіші
 int pinTMP36=A1; 
 // Фоторезистордың аналогтық шығысын қосуға арналған түйреуіш
 int pinPhotoresistor=A2;

// DHT нысанының данасын жасау
 DHT dht(pinDHT11, DHTTYPE);

void setup() 
{ 
 // сериялық портты іске қосу
 Serial.begin(9600);
 dht.begin();
 }

жарамсыз цикл() 
{ 
 // DHT11 арқылы деректерді алу
 қалқымалы h = dht.readHumidity(); 
 егер (isnan(h)) 
{ 
 Serial.println("DHT-тен оқу сәтсіз аяқталды"); 
} 
басқа 
{ 
 Serial.print("HumidityDHT11= "); Serial.print(h);Serial.println(" %"); 
} 
 // топырақ ылғалдылығы модулінің аналогтық шығысынан мәнді алу
 int val0=analogRead(pinSoilMoisture);
 Serial.print("SoilMoisture= "); Serial.println(val0);
 // TMP36 температура сенсорының аналогтық шығысынан мәнді алу
 int val1=analogRead(pinTMP36); 
 // мВ-ға аудару
 int mV=val1*1000/1024; 
 // Цельсий градусына аудару
 int t=(mV-500)/10;
 Serial.print("TempTMP36= "); Serial.print(h);Serial.println(" C"); 
 // фоторезистордың аналогтық терминалынан мән алу
 int val2=analogRead(pinPhotoresistor);
 Serial.print("Light= "); Serial.println(val2);
 // 5 секунд үзіліс
 Serial.println( );
 delay(5000);
 }
