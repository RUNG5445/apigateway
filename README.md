# คู่มือการใช้งาน API

URL หลัก: http://rung.ddns.net:8050

## 1. หน้าแรก (API Portal)
- API Endpoint: /
- HTTP Method: GET
- คำอธิบาย:  Endpoint นี้ใช้สำหรับการเข้าถึง Endpoint API ต่างๆ โดยจะคืนหน้า Portalพร้อมลิงก์ไปยัง API Endpoint นั้นๆ

ตัวอย่างการร้องขอ:
```http 
GET http://rung.ddns.net:8050/
```

ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: เนื้อหา HTML สำหรับหน้าแรกพร้อมลิงก์ไปยัง Endpoint API ต่างๆ

## 2. แทรกข้อมูล
- API Endpoint: /api/data
- HTTP Method: POST
- คำอธิบาย: Endpoint นีใช้ในการแทรกข้อมูลที่ได้มาจากลงในฐานข้อมูล MySQL

ตัวอย่างการร้องขอ:
```http 
POST http://rung.ddns.net:8050/api/data
```
ข้อมูลที่ต้องใช้สำหรับการร้องขอ:
```json
{
  "nodename": "Node1",
  "temperature": 25.5,
  "humidity": 50.2,
  "latitude": 12.345,
  "longitude": 67.890
}
```
ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: "แทรกข้อมูลเรียบร้อย" (หากการแทรกข้อมูลเสร็จสมบูรณ์)
- รหัสสถานะ: 400 Bad Request
- ตอบกลับ: "ข้อมูลไม่ถูกต้อง" (หากข้อมูลในคำร้องขอในบางฟิลด์ที่จำเป็นขาดหายไป)

## 3. กำหนดค่า
- API Endpoint: /api/config
- HTTP Method: GET
- คำอธิบาย: ใช้ Endpoint นี้ในการกำหนดค่า LoRa parameter ต่างๆ

ตัวอย่างการร้องขอ:
```http 
GET http://rung.ddns.net:8050/api/config
```

ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: เนื้อหา HTML สำหรับการกำหนดค่า LoRa parameter ต่างๆ

## 4. ปรับปรุงการกำหนดค่า
- API Endpoint: /sendconfig
- HTTP Method: POST
- คำอธิบาย: ใช้ Endpoint นี้ในการปรับปรุงค่า LoRa parameter ต่างๆ

ตัวอย่างการร้องขอ:
```http 
POST http://rung.ddns.net:8050/sendconfig
```
ข้อมูลที่ต้องใช้สำหรับการร้องขอ:
```json
{
  "syncword": 140,
  "txPower": 12,
  "freq": 920,
  "interval": 30
}
```
ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: "แทรกข้อมูลเรียบร้อย" (หากการแทรกข้อมูลเสร็จสมบูรณ์)
- รหัสสถานะ: 400 Bad Request
- ตอบกลับ: "ข้อมูลไม่ถูกต้อง" (หากข้อมูลในคำร้องขอในบางฟิลด์ที่จำเป็นขาดหายไป)

## 5. แสดงข้อมูลทั้งหมด
- API Endpoint: /api/show
- HTTP Method: GET
- คำอธิบาย: ดึงและแสดงข้อมูลทั้งหมดจากฐานข้อมูล MySQL

ตัวอย่างการร้องขอ:
```http 
GET http://rung.ddns.net:8050/api/show
```
ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: ข้อมูลทั้งหมดจากฐานข้อมูล MySQL ในรูปแบบ JSON
- ข้อมูล JSON จากการตอบกลับ:
  
```json

[
  {  
    "Time": "2023-10-13 11:37:59",
    "Nodename": "Node 1",
    "Temperature": 25.0,
    "Humidity": 50.0,
    "Latitude": 13.736717,
    "Longitude": 100.536144
  },
  {
    "Time": "2023-10-13 11:38:00",
    "Nodename": "Node 2",
    "Temperature": 26.0,
    "Humidity": 60.0,
    "Latitude": 13.736718,
    "Longitude": 100.536145
  }
]

```

## 6. ลบข้อมูล
- API Endpoint: /api/delete
- HTTP Method: GET
- คำอธิบาย: ใช้ Endpoint นี้ในการลบข้อมูลทั้งหมดออกจากฐานข้อมูล MySQL

ตัวอย่างการร้องขอ:
```http 
GET http://rung.ddns.net:8050/api/delete
```
ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: "ลบข้อมูลเรียบร้อย"

## 7. สร้างแผนที่
- API Endpoint: /map
- HTTP Method: GET
- คำอธิบาย: สร้างและแสดงแผนที่พร้อมเครื่องหมายที่แทนจุดข้อมูลที่ตำแหน่งต่างๆ

ตัวอย่างการร้องขอ:
```http 
GET http://rung.ddns.net:8050/map
```
ตัวอย่างการตอบกลับ:
- รหัสสถานะ: 200 OK
- ตอบกลับ: เนื้อหา HTML ที่แสดงแผนที่พร้อมเครื่องหมายสำหรับจุดข้อมูลที่ตำแหน่งต่างๆ


