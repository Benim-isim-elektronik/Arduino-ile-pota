/*Benim İşim Elektronik Youtube Kanalı
 Arduino ile Pota yapımı */
#include <LiquidCrystal.h> //lcd ekran Kütüphanesi
LiquidCrystal lcd(12,11,5,4,3,2);//Lcd ekran bağlantı pinleri

const int trig =9; //Hcr-04 sensör trig pini
const int echo =8; //Hcr-04 sensör echo pini
const int LED =13; //basket olduğunda yanan led pini

int mesafe; //Hcr sensörünün süresi sonucnda bulduğumuz mesafe değeri
int sure; //Ses dalgasının gidiş geliş süresi
int sayi = 0;


void setup() {
  //Pinleri giriş ve çıkış olarak tanımlıyoruz
 pinMode(trig,OUTPUT);
 pinMode(echo, INPUT);
 pinMode(LED, OUTPUT);

 lcd.begin(16, 2); // 16 sütun 2 satırdan oluşuyor
void loop() {
 digitalWrite(trig, HIGH);
 delay(1);
 digitalWrite(trig, LOW);
 sure = pulseIn(echo, HIGH);
 mesafe =(sure/2)/29,1;//29.1 degeri ortamın sıcaklıgına göre belirlenir

 lcd.home();
 if(mesafe<=10)//Burdaki 10 cm potanın kesilen kısmının uzunluğudur. Siz kendiniz ölçüp yazmalısınız.
 {
  sayi +=1; 
  digitalWrite(LED,HIGH);
  lcd.print("ATILAN BASKET ");
  lcd.setCursor(0,1);//0.sütun 1.satıra ayarlanıyor 
  lcd.print(sayi);
  lcd.print("  OLDU");
  delay(250);
  
  }
  else
  {
    digitalWrite(LED,LOW);
    }

}
