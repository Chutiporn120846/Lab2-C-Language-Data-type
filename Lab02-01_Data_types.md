# ใบงานที่ 02.01 การประกาศและแสดงผลชนิดข้อมูลพื้นฐาน

## ขั้นตอนการทดลอง


### 1. เปิด Wokwi และเตรียมโปรเจกต์

- ไปที่เว็บไซต์ https://wokwi.com/

- เข้าสู่ระบบหรือสร้างบัญชีใหม่ (แนะนำให้ใช้บัญชี Google เพื่อความสะดวก)

- คลิกที่บอร์ด  ESP32 Dev Module

- เลื่อนลงมาที่ Starter Templates แล้วเลือก ESP32

- ในไฟล์ ino ที่เปิดขึ้นมา ให้ลบโค้ดเริ่มต้นที่ไม่ได้ใช้ออก โดยคงเหลือเพียงโครงสร้างพื้นฐานของ `setup()` และ `loop()` ไว้ดังนี้:

``` c
void setup() {

}

void loop() {

}
```

- ในฟังก์ชัน `setup()` ให้เพิ่ม `Serial.begin(115200);` เพื่อเริ่มต้นการสื่อสารผ่าน Serial Monitor (สำหรับ ESP32 นิยมใช้ Baud Rate ที่สูง ๆ  เช่น 115200)

### 2. ทดลองกับ int (จำนวนเต็ม):

__วัตถุประสงค์__ 

ทำความเข้าใจการเก็บค่าจำนวนเต็มและขอบเขตของ int บน ESP32

__หมายเหตุ__ 

บน ESP32 (ซึ่งเป็นสถาปัตยกรรม 32-bit) ชนิด int จะมีขนาด 4 ไบต์ (32 บิต) ทำให้มีขอบเขตที่กว้างกว่า Arduino Uno (8-bit, int ขนาด 2 ไบต์)

- เพิ่มโค้ดต่อไปนี้ใน `setup()`  

__ระวัง__ อย่าลบโค้ด `Serial.begin()`

``` c
// ส่วนที่ 2.1
Serial.println("--- ทดสอบชนิดข้อมูล int (ESP32) ---");
int myInteger = 100;
Serial.print("ค่าเริ่มต้นของ myInteger: ");
Serial.println(myInteger);


// ส่วนที่ 2.2
// ลองกำหนดค่าให้เกินขอบเขตสูงสุดของ int (ประมาณ 2,147,483,647 สำหรับ 32-bit int)
myInteger = 2147483647; // ค่าสูงสุด
Serial.print("myInteger = 2147483647 ผลลัพธ์: ");
Serial.println(myInteger);

// ส่วนที่ 2.3
myInteger = 2147483647 + 1; // ลองเกินค่าสูงสุด
Serial.print("myInteger = 2147483647 + 1 ผลลัพธ์: ");
Serial.println(myInteger); // สังเกตผลลัพธ์ที่อาจเกิด Overflow

// ส่วนที่ 2.4
// ลองกำหนดค่าให้ต่ำกว่าขอบเขตต่ำสุดของ int (ประมาณ -2,147,483,648 สำหรับ 32-bit int)
myInteger = -2147483648; // ค่าต่ำสุด
Serial.print("myInteger = -2147483648 ผลลัพธ์: ");
Serial.println(myInteger);

// ส่วนที่ 2.5
myInteger = -2147483648 - 1; // ลองต่ำกว่าค่าต่ำสุด
Serial.print("myInteger = -2147483648 - 1 ผลลัพธ์: ");
Serial.println(myInteger); // สังเกตผลลัพธ์ที่อาจเกิด Underflow
```

- ดำเนินการกดปุ่ม "Start Simulation" แล้วเปิด "Serial Monitor" (อยู่ด้านล่างของหน้าจอ Wokwi) เพื่อดูผลลัพธ์


__คำถาม__

2.1  สังเกตผลจากการรันโคิดในส่วน 2.1 ว่าตรงตามหลักการทางคณิตศาสตร์หรือไม่ เพราะเหตุใด


2.2  สังเกตผลจากการรันโคิดในส่วน 2.2 ว่าตรงตามหลักการทางคณิตศาสตร์หรือไม่ เพราะเหตุใด


2.3  สังเกตผลจากการรันโคิดในส่วน 2.3 ว่าตรงตามหลักการทางคณิตศาสตร์หรือไม่ เพราะเหตุใด


2.4  สังเกตผลจากการรันโคิดในส่วน 2.4 ว่าตรงตามหลักการทางคณิตศาสตร์หรือไม่ เพราะเหตุใด


2.5  สังเกตผลจากการรันโคิดในส่วน 2.5 ว่าตรงตามหลักการทางคณิตศาสตร์หรือไม่ เพราะเหตุใด


### 3. ทดลองกับ float และ double (ทศนิยม)

__วัตถุประสงค์__ 

ทำความเข้าใจการเก็บค่าทศนิยมและความแม่นยำของ float และ double บน ESP32

__หมายเหตุ__ 

บน ESP32, float คือ 4 ไบต์ (Single Precision) และ double คือ 8 ไบต์ (Double Precision) ซึ่งมีความแม่นยำสูงกว่า

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`

``` c
// ส่วนที่ 3.1
Serial.println("\n--- ทดสอบชนิดข้อมูล float และ double (ESP32) ---");
float myFloat = 3.14159265; // ค่า Pi
Serial.print("ค่า myFloat (float): ");
Serial.println(myFloat, 8); // แสดงผลทศนิยม 8 ตำแหน่ง

// ส่วนที่ 3.2
double myDouble = 3.141592653589793; // ค่า Pi ที่แม่นยำกว่า
Serial.print("ค่า myDouble (double): ");
Serial.println(myDouble, 15); // แสดงผลทศนิยม 15 ตำแหน่ง
```


- ดำเนินการกด "Stop Simulation" ก่อน แล้วค่อย "Start Simulation" ใหม่

__คำถาม__ 

3.1 คุณสังเกตเห็นความแตกต่างของความแม่นยำระหว่าง float และ double อย่างไร? 

3.2 สถานการณ์ใดที่คุณควรเลือกใช้ double แทน float?

### 4. ทดลองกับ char (อักขระ)

__วัตถุประสงค์__ 

ทำความเข้าใจการเก็บอักขระและการแปลงเป็นค่า ASCII

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);`


``` c
// ส่วนที่ 4.1
Serial.println("\n--- ทดสอบชนิดข้อมูล char ---");
char myChar = 'Z';
Serial.print("myChar = 'Z' ผลลัพธ์: ");
Serial.println(myChar);
Serial.print("myChar ในรูป ASCII: ");
Serial.println((int)myChar); // แปลง char เป็น int เพื่อดูค่า ASCII

// ส่วนที่ 4.2
myChar = 122; // 122 คือค่า ASCII ของ 'z'
Serial.print("myChar = 122 ผลลัพธ์: ");
Serial.println(myChar);
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว

__คำถาม__ 

4.1 ค่าตัวเลข (ASCII value) มีความสัมพันธ์กับอักขระอย่างไร?

4.2 ถ้าอยากทราบความสัมพันธ์ระหว่างตัวเลขกับอักขระทั้งหมด สามารถหาได้จากเอกสารใด หรือแหล่งอ้างอิงใด

4.3 จากข้อ 4.2 นักเขียนโปรแกรมสามารถกำหนดขึ้นเองได้ หรือมีเอกสารใดกำกับอยู่


### 5. ทดลองกับ bool (ตรรกะ)

__วัตถุประสงค์__

ทำความเข้าใจการเก็บค่าความจริง (true หรือ false)

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);` 

``` c
// ส่วนที่ 5.1
Serial.println("\n--- ทดสอบชนิดข้อมูล bool ---");
bool myBool = true;
Serial.print("myBool = true ผลลัพธ์: ");
Serial.println(myBool); // true จะถูกแสดงเป็น 1

// ส่วนที่ 5.1
myBool = false;
Serial.print("myBool = false ผลลัพธ์: ");
Serial.println(myBool); // false จะถูกแสดงเป็น 0
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว

__คำถาม__ 

5.1 true และ false ถูกแสดงผลเป็นค่าใดบน Serial Monitor?

### 6. ทดลองกับ long, long long, unsigned int, unsigned long, unsigned long long (จำนวนเต็มขนาดใหญ่/ไม่มีเครื่องหมาย)

__วัตถุประสงค์__

ทำความเข้าใจการใช้ชนิดข้อมูลสำหรับจำนวนเต็มที่มีขนาดใหญ่ขึ้นและแบบไม่มีเครื่องหมายบน ESP32

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);` 

``` c
Serial.println("\n--- ทดสอบชนิดข้อมูล long, long long, unsigned (ESP32) ---");

long myLong = 4000000000L; // long บน ESP32 คือ 32-bit (เท่า int)
Serial.print("myLong (4,000,000,000): ");
Serial.println(myLong); // จะเกิด overflow เพราะเกิน 2.1 พันล้าน

long long myLongLong = 9000000000000000000LL; // long long คือ 64-bit
Serial.print("myLongLong (9,000,000,000,000,000,000): ");
Serial.println(myLongLong);

unsigned int myUnsignedInt = 4000000000U; // unsigned int คือ 32-bit
Serial.print("myUnsignedInt (4,000,000,000): ");
Serial.println(myUnsignedInt);

unsigned long myUnsignedLong = 4000000000UL; // unsigned long คือ 32-bit
Serial.print("myUnsignedLong (4,000,000,000): ");
Serial.println(myUnsignedLong);

unsigned long long myUnsignedLongLong = 18000000000000000000ULL; // unsigned long long คือ 64-bit
Serial.print("myUnsignedLongLong (1.8e19): ");
Serial.println(myUnsignedLongLong);

```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว

__คำถาม__ 

6.1 บน ESP32, long มีขอบเขตเท่ากับ int หรือไม่? 

6.2 ชนิดข้อมูลใดที่ต้องใช้หากต้องการเก็บค่าจำนวนเต็มบวกที่ใหญ่ที่สุด?

### 7. ทดลองกับ byte (ข้อมูล 8 บิต)

__วัตถุประสงค์__

ทำความเข้าใจการเก็บค่าจำนวนเต็มขนาดเล็ก (0-255)

- โค้ดที่ต้องเพิ่มใน `setup()` โดยลบโค้ดเดิมออก ยกเว้นบรรทัด `Serial.begin(115200);` 

``` c 
Serial.println("\n--- ทดสอบชนิดข้อมูล byte ---");
byte myByte = 250;
Serial.print("myByte = 250 ผลลัพธ์: ");
Serial.println(myByte);

myByte = 256; // ค่าเกินขอบเขต (0-255)
Serial.print("myByte = 256 ผลลัพธ์: ");
Serial.println(myByte); // สังเกตผลลัพธ์
```

- ดำเนินการจำลองตามวิธีที่ได้ทดลองมาแล้ว

__คำถาม__ 

- เมื่อ myByte ถูกกำหนดให้เป็น 256 ผลลัพธ์ที่ได้คืออะไร และเพราะเหตุใด?
