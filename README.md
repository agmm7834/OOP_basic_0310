Python OOP (Ob'ektga Yo'naltirilgan Dasturlash) 
---
1. Eng Sodda Klass va Ob'ekt Yaratish
Dastlab, hech qanday ichki parametrlarsiz eng sodda klass yaratamiz.
Klass — bu xususiyat va harakatlarni jamlovchi qolip (shablon).
Ob'ekt — shu qolipdan yaratilgan nusxa.
```python
# 1-qadam: Bo'sh klass yaratish
class Inson:
    pass  # pass - hozircha klass ichi bo'sh degani

# 2-qadam: Ob'ekt yaratish
odam1 = Inson()
odam2 = Inson()

print(odam1)  # Ob'ekt xotiradagi manzili bilan ko'rinadi
print(odam2)
```
---
2. Klass Atributlari (Class Attributes)
Klass atributi — bu klass ichida joylashgan va shu klassdan yaratiladigan barcha ob'ektlar uchun umumiy bo'lgan o'zgaruvchidir.
```python
class Moshina:
    # Klass atributi (Barcha moshinalar uchun g'ildiraklar soni 4 ta)
    gildiraklar_soni = 4
    yoqilgi = "Benzin"

# Ob'ektlar yaratamiz
damas = Moshina()
nexia = Moshina()

# Klass atributlariga murojaat qilish
print("Damas g'ildiraklar soni:", damas.gildiraklar_soni)
print("Nexia yoqilg'i turi:", nexia.yoqilgi)

# Klass nomi orqali ham murojaat qilish mumkin:
print("Umumiy g'ildiraklar soni:", Moshina.gildiraklar_soni)
```
---
3. Konstruktor (`__init__()` metodi) va Ob'ekt Atributlari
Har bir ob'ektning o'ziga xos (shaxsiy) xususiyatlari bo'ladi. Masalan, har bir insonda ism va yosh har xil.
`__init__()` — bu konstruktor (initsializator). Yangi ob'ekt yaratilishi bilan ushbu metod avtomati ravishda ishga tushadi.
> **`self` nima?**  
> `self` — yaratilayotgan **ob'ektning o'ziga** ishora qiluvchi kalit so'z.
```python
class Talaba:
    def __init__(self, ism, yosh):
        # self.ism va self.yosh - ob'ektning shaxsiy atributlari
        self.ism = ism
        self.yosh = yosh

# Ob'ekt yaratamiz va ularga shaxsiy qiymatlarni beramiz
talaba1 = Talaba("Ali", 20)
talaba2 = Talaba("Vali", 22)

# Har bir ob'ektning shaxsiy ma'lumotlarini o'qiymiz
print(f"1-talaba: {talaba1.ism}, Yoshi: {talaba1.yosh}")
print(f"2-talaba: {talaba2.ism}, Yoshi: {talaba2.yosh}")
```
---
4. Klass Metodlari (Klass ichidagi funksiyalar)
Metod — klass ichida yoziladigan va ob'ekt bajarishi mumkin bo'lgan harakat yoki operatsiya hisoblanadi.
```python
class ITParkOquvchisi:
    # Klass atributi
    markaz = "IT Park"

    # Konstruktor
    def __init__(self, ism, kurs):
        self.ism = ism
        self.kurs = kurs

    # Metod 1: O'zi haqida ma'lumot beruvchi metod
    def tanishuv(self):
        print(f"Salom, mening ismim {self.ism}. Men {self.kurs} yo'nalishida o'qiyman.")

    # Metod 2: Darsga qatnashish harakati
    def dars_qil(self):
        print(f"{self.ism} hozir {self.kurs} darsini topshirmoqda...")


# Ob'ektlar yaratamiz
oquvchi1 = ITParkOquvchisi("Anvar", "Python")
oquvchi2 = ITParkOquvchisi("Malika", "Web-Design")

# Metodlarni ishlatamiz
oquvchi1.tanishuv()
oquvchi1.dars_qil()

print("-" * 30)

oquvchi2.tanishuv()
oquvchi2.dars_qil()
```
---
5. Metodlar orqali Atributlarni O'zgartirish
Metodlar yordamida ob'ekt atributlarining qiymatini o'zgartirish va hisob-kitoblar qilish mumkin.
```python
class Telefon:
    def __init__(self, model, batareya):
        self.model = model
        self.batareya = batareya # % da

    # Batareya quvvatini ko'rsatish
    def quvvatni_kor(self):
        print(f"{self.model} quvvati: {self.batareya}%")

    # O'yin o'ynaganda batareya kamayadi
    def oyin_oyna(self, soat):
        kamayish = soat * 15
        self.batareya -= kamayish
        if self.batareya < 0:
            self.batareya = 0
        print(f"{soat} soat o'yin o'ynaldi. Batareya {self.batareya}% qoldi.")

    # Quvvatlash metodi
    def zaryadla(self):
        self.batareya = 100
        print(f"{self.model} to'liq quvvatlandi (100%).")


# Sinab ko'ramiz
phone = Telefon("Redmi", 80)

phone.quvvatni_kor()
phone.oyin_oyna(3)   # 3 soat o'ynalganda 45% kamayadi
phone.quvvatni_kor()
phone.zaryadla()
```
---
6. Barchasini Jamlagan Amaliy Misol: "Bank Hisobi"
Quyida real hayotda ishlatiladigan sodda Bank hisobi (Card) klassi ko'rsatilgan:
```python
class BankKartasi:
    # Klass atributi
    valyuta = "SO'M"

    def __init__(self, egasi, karta_raqam, balans=0):
        self.egasi = egasi
        self.karta_raqam = karta_raqam
        self.balans = balans

    # Pul kiritish metodi
    def pul_toldir(self, summa):
        self.balans += summa
        print(f"Hisobga {summa} {BankKartasi.valyuta} qo'shildi.")
        print(f"Joriy balans: {self.balans} {BankKartasi.valyuta}")

    # Pul yechish metodi
    def pul_yech(self, summa):
        if summa <= self.balans:
            self.balans -= summa
            print(f"Hisobdan {summa} {BankKartasi.valyuta} yechildi.")
            print(f"Qolgan balans: {self.balans} {BankKartasi.valyuta}")
        else:
            print("Xatolik: Hisobingizda yetarli mablag' mavjud emas!")

    # Malumotlarni ko'rsatish
    def info(self):
        print(f"Ega: {self.egasi} | Karta: {self.karta_raqam} | Balans: {self.balans} {self.valyuta}")


# Dasturni ishlatib ko'ramiz:
karta1 = BankKartasi("Jasur", "8600 **** **** 1234", 50000)

karta1.info()
karta1.pul_toldir(100000)
karta1.pul_yech(30000)
karta1.pul_yech(200000) # Balans yetmaydigan holat
```
---
Qisqacha Xulosa
`class ClassName:` — Yangi klass yaratish strukturasi.
`Klass atributi` — Hamma ob'ektlar uchun bir xil va umumiy.
`def __init__(self, ...):` — Ob'ekt ishga tushishi bilan birinchi bo'lib ishlaydigan tayyorlovchi metod.
`self` — Aynan o'sha ob'ektning o'ziga berilgan murojaat.
`Ob'ekt atributi` — `self.atribut_nomi` orqali yaratiladi va har bir ob'ektda har xil bo'ladi.
