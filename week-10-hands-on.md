# Minggu 10 – Hands in Database Tuning  
### PostgreSQL: Indexing dan Optimasi Performa  
**Durasi:** ±45–60 menit  
**Konteks:** Simulasi database UMKM (E-Commerce Sederhana)

---

## 🎯 Tujuan Pembelajaran
Setelah mengikuti praktikum ini, mahasiswa diharapkan dapat:
- Memahami konsep dasar **query tuning** dan **indexing** pada PostgreSQL.  
- Mampu menggunakan `EXPLAIN` dan `EXPLAIN ANALYZE` untuk mengukur performa query.  
- Melihat secara langsung perbedaan waktu eksekusi sebelum dan sesudah dilakukan tuning.

---

## 🧩 Lingkungan Praktikum
- **Database:** PostgreSQL 14+  
- **Tools:** pgAdmin / psql  
- **Koneksi:** Lokal (tidak butuh internet)  
- **Spesifikasi:** Laptop 4–8 GB RAM  

---

## 🧱 Langkah-Langkah Praktikum

```sql
-- ============================================================
-- PRAKTIKUM: Database Tuning dan Index Performance
-- Durasi: ±45–60 menit
-- Konteks: Database “Orders” ala UMKM (e-commerce sederhana)
-- ============================================================

-- 1️⃣  BUAT DATABASE (jika belum ada)
CREATE DATABASE tuning_lab;
\c tuning_lab

-- 2️⃣  BUAT TABEL SEDERHANA
CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    city VARCHAR(100),
    join_date DATE
);

CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES customers(id),
    order_date DATE,
    total_amount NUMERIC(10,2),
    status VARCHAR(20)
);

-- 3️⃣  ISI DATA CONTOH (simulasi data UMKM)
-- Catatan: ubah jumlah data jika ingin lebih kecil (misal 10_000 baris)
INSERT INTO customers (name, city, join_date)
SELECT 
    'Customer ' || i,
    CASE WHEN i % 5 = 0 THEN 'Surabaya'
         WHEN i % 5 = 1 THEN 'Malang'
         WHEN i % 5 = 2 THEN 'Jakarta'
         WHEN i % 5 = 3 THEN 'Solo'
         ELSE 'Bandung' END,
    NOW() - (i || ' days')::interval
FROM generate_series(1, 1000) AS s(i);

INSERT INTO orders (customer_id, order_date, total_amount, status)
SELECT 
    (RANDOM() * 999 + 1)::INT,
    NOW() - (RANDOM() * 365 || ' days')::interval,
    ROUND(RANDOM() * 100000, 2),
    CASE WHEN RANDOM() < 0.7 THEN 'paid' ELSE 'pending' END
FROM generate_series(1, 100000) s(i);

-- 4️⃣  JALANKAN QUERY LAMBAT (tanpa index)
EXPLAIN ANALYZE
SELECT c.city, COUNT(*) AS total_orders, SUM(o.total_amount) AS revenue
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.status = 'paid' AND c.city = 'Surabaya'
GROUP BY c.city;

-- ⏱ Catat waktu eksekusi dari EXPLAIN ANALYZE
-- Biasanya butuh beberapa detik tergantung spesifikasi laptop.

-- 5️⃣  BUAT INDEX UNTUK MENINGKATKAN KINERJA
CREATE INDEX idx_orders_status ON orders(status);
CREATE INDEX idx_customers_city ON customers(city);
CREATE INDEX idx_orders_customer ON orders(customer_id);

-- 6️⃣  JALANKAN LAGI QUERY YANG SAMA
EXPLAIN ANALYZE
SELECT c.city, COUNT(*) AS total_orders, SUM(o.total_amount) AS revenue
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.status = 'paid' AND c.city = 'Surabaya'
GROUP BY c.city;

-- Amati:
--   🔹 Waktu query harus turun signifikan (bisa 80–95% lebih cepat)
--   🔹 Rencana eksekusi (plan) berubah jadi Index Scan

-- 7️⃣  OPSIONAL: Paksa PostgreSQL pakai sequential scan
SET enable_seqscan = off;
EXPLAIN ANALYZE
SELECT c.city, COUNT(*) AS total_orders, SUM(o.total_amount) AS revenue
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.status = 'paid' AND c.city = 'Surabaya'
GROUP BY c.city;
RESET enable_seqscan;

-- 8️⃣  BERSIHKAN DATABASE (opsional)
-- DROP DATABASE tuning_lab;
