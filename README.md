# LED Kontrol Projesi

Bu proje, Arduino kullanarak seri iletişim yoluyla LED'leri kontrol etmeyi amaçlar. Kullanıcıdan alınan komutlara göre kırmızı, sarı ve yeşil LED'lerin durumları değiştirilir.

## İçindekiler

- [Açıklama](#açıklama)
- [Gereksinimler](#gereksinimler)
- [Kurulum](#kurulum)
- [Kullanım](#kullanım)
- [Kod Açıklaması](#kod-açıklaması)

## Açıklama

Bu proje, Arduino kartı ve üç adet LED (kırmızı, sarı, yeşil) kullanılarak basit bir trafik ışığı kontrol sistemi oluşturur. Seri port üzerinden gönderilen komutlar ile LED'lerin yanma durumları kontrol edilebilir.

## Gereksinimler

- Arduino kartı
- 3 adet LED (kırmızı, sarı, yeşil)
- 3 adet direnç (220-330 ohm)
- Breadboard
- Jumper kabloları
- Arduino IDE

## Kurulum

1. LED'leri breadboard'a yerleştirin ve her bir LED'in katot ucunu (kısa bacak) bir direnç üzerinden GND'ye bağlayın.
2. LED'lerin anot uçlarını (uzun bacak) Arduino kartının dijital pinlerine (kırmızı: 4, sarı: 5, yeşil: 6) bağlayın.
3. Arduino kartını bilgisayara bağlayın.
4. Arduino IDE'yi açın ve kodu yükleyin.

## Kullanım

1. Arduino IDE'nin seri monitörünü açın.
2. Seri monitöre aşağıdaki komutları girerek LED'leri kontrol edebilirsiniz:
   - `dur`: Kırmızı LED yanar, diğerleri söner.
   - `hazirlan`: Sarı LED yanar, diğerleri söner.
   - `gec`: Yeşil LED yanar, diğerleri söner.
  ![Image](https://github.com/user-attachments/assets/36ab155f-4d8a-4a34-aec4-75d887802c4b)

## Kod Açıklaması

```c++
String komut; // Klavyeden girilen komutu belirtmek için tanımladık.
int kirmizi = 4; // Kırmızı LED'i 4. pine bağladık ve tanımladık.
int sari = 5; // Sarı LED'i 5. pine bağladık ve tanımladık.
int yesil = 6; // Yeşil LED'i 6. pine bağladık ve tanımladık.

void setup() {
  Serial.begin(9600); // Seri iletişimi başlattık.
  pinMode(kirmizi, OUTPUT); // 4. pinden kırmızı LED'e çıkış verdik.
  pinMode(sari, OUTPUT); // 5. pinden sarı LED'e çıkış verdik.
  pinMode(yesil, OUTPUT); // 6. pinden yeşil pine çıkış verdik.
}

void loop() {
  if (Serial.available()) { // Veri geliyorsa uygulanacak işlemleri if ile belirttik.
    komut = Serial.readString(); // Girilen değeri komut değişkenine ata.
    if (komut == "dur") { // Komut değişkeni "dur" ise...
      digitalWrite(kirmizi, HIGH); // Kırmızı LED'i yak.
      digitalWrite(sari, LOW); // Sarı LED'i söndür.
      digitalWrite(yesil, LOW); // Yeşil LED'i söndür.
    }
    if (komut == "hazirlan") { // Komut değişkeni "hazirlan" ise...
      digitalWrite(kirmizi, LOW); // Kırmızı LED'i söndür.
      digitalWrite(sari, HIGH); // Sarı LED'i yak.
      digitalWrite(yesil, LOW); // Yeşil LED'i söndür.
    }
    if (komut == "gec") { // Komut değişkeni "gec" ise...
      digitalWrite(kirmizi, LOW); // Kırmızı LED'i söndür.
      digitalWrite(sari, LOW); // Sarı LED'i söndür.
      digitalWrite(yesil, HIGH); // Yeşil LED'i yak.
    }
  }
}
