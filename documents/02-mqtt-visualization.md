# 📊 **Overview: VerneMQ + Prometheus + Grafana Integration**

### 🧭 **วัตถุประสงค์**

* **VerneMQ**: ทำหน้าที่เป็น MQTT broker ที่ให้ข้อมูล metrics ภายใน
* **Prometheus**: ทำหน้าที่ดึง (scrape) metrics จาก VerneMQ มาเก็บไว้
* **Grafana**: แสดงผลกราฟสวยงามด้วย dashboard ที่ดึงข้อมูลจาก Prometheus

---

## 🔗 **1. VerneMQ → Prometheus**

### 📌 ปกติ VerneMQ **ไม่มี Prometheus exporter** ติดมากับ container image โดยตรง

#### ✅ **ใช้ VerneMQ Prometheus Plugin (official)**

* ปลั๊กอินนี้สามารถเปิดใช้งานใน VerneMQ ได้ และจะ expose endpoint เช่น:

  ```
  http://<vernemq_host>:8888/metrics
  ```

* เพิ่ม env ลงใน `docker-compose.yml`:

```yaml
- DOCKER_VERNEMQ_PROMETHEUS__ENABLED=on
```

---

## 📥 **2. Prometheus ← Scrapes VerneMQ**

ใน `prometheus.yml` (mounted เข้า container Prometheus), ให้เพิ่ม job:

```yaml
scrape_configs:
  - job_name: 'vernemq'
    metrics_path: /metrics
    static_configs:
      - targets: ['vernemq1.local:8888']
```

> ✅ หมายเหตุ: `vernemq1.local:8888` ต้องเป็นชื่อหรือ IP ที่ Prometheus container มองเห็นได้ (อยู่ใน network เดียวกัน)

---

## 📈 **3. Grafana ← Queries Prometheus**

### ขั้นตอน:

1. เปิด Grafana ที่ `http://localhost:3000`
2. Login (admin/admin หรือที่ตั้งไว้)
3. ไปที่ ⚙️ **Configuration → Data Sources**
4. Add new data source → เลือก Prometheus
5. ตั้ง `URL = http://prometheus:9090` (ชื่อ container `prometheus`)
6. Save & Test ✅

### 📊 โหลด Dashboard:

* สร้างใหม่หรือ Import dashboard ที่ใช้ query เช่น:

```promql
vernemq_subscriptions_total
vernemq_sessions_max
vernemq_retained_messages
vernemq_bytes_received
```

---

## 🔁 **Flow การไหลของข้อมูล**

```
[ IoT Devices ]
       ↓
   (MQTT Data)
       ↓
   [ VerneMQ Broker ]
       ↓
  (metrics exposed at /metrics)
       ↓
  [ Prometheus ]
       ↓
   (query via PromQL)
       ↓
   [ Grafana Dashboard ]
```

---

## ✅ ตัวอย่าง Metrics ที่น่าสนใจจาก VerneMQ

| Metric Name                    | Description                              |
| ------------------------------ | ---------------------------------------- |
| `vernemq_subscriptions_total`  | Total number of subscriptions            |
| `vernemq_clients_connected`    | Number of currently connected clients    |
| `vernemq_bytes_received_total` | Total bytes received                     |
| `vernemq_messages_in_total`    | Number of messages received from clients |
| `vernemq_messages_out_total`   | Number of messages published to clients  |

---

## 💡 สรุปภาพรวม

| Component      | Role                                                     |
| -------------- | -------------------------------------------------------- |
| **VerneMQ**    | MQTT broker + exposes internal metrics (`/metrics`)      |
| **Prometheus** | Pulls (scrapes) metrics from VerneMQ regularly           |
| **Grafana**    | Reads data from Prometheus and visualizes via dashboards |

---
