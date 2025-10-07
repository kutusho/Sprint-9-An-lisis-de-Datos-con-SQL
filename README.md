# Sprint 9 – Análisis de Datos con SQL

## 📄 Descripción
Proyecto desarrollado durante el **Sprint 9 del Bootcamp de Data Analytics – TripleTen**, enfocado en la **extracción, transformación y análisis de datos usando SQL**.  
El objetivo principal fue obtener insights sobre el comportamiento de usuarios y la eficiencia de las campañas de marketing de una plataforma digital, aplicando consultas SQL avanzadas para resolver problemas de negocio reales.

---

## 🎯 Objetivo
Analizar la información almacenada en una base de datos relacional y responder preguntas clave sobre adquisición, retención y rentabilidad, utilizando **consultas SQL optimizadas y reproducibles**.

---

## 🧩 Contexto del caso
Una empresa de contenidos digitales quiere evaluar el desempeño de sus campañas de suscripción.  
Los datos incluyen información de **usuarios, pedidos, sesiones y fuentes de tráfico** en múltiples tablas conectadas mediante claves foráneas.

---

## 🧠 Metodología

1. **Exploración de la base de datos**
   - Revisión del esquema relacional y relaciones entre tablas (`users`, `orders`, `subscriptions`, `traffic_source`).  
   - Identificación de llaves primarias y foráneas.

2. **Consultas SQL principales**
   - **JOINs** (INNER, LEFT) para combinar información de usuarios y pedidos.  
   - **Subconsultas y CTEs (WITH)** para calcular métricas derivadas.  
   - **Funciones de agregación:** `COUNT`, `AVG`, `SUM`, `ROUND`, `MAX`, `MIN`.  
   - **Funciones de ventana:** `ROW_NUMBER()`, `RANK()`, `LAG()`, `OVER(PARTITION BY ...)`.

3. **Métricas calculadas**
   - Número total de usuarios activos por mes.  
   - Tasa de conversión por canal de adquisición.  
   - Ingresos totales y promedio por cliente (ARPU / LTV).  
   - Análisis de churn y retención mensual.  

4. **Visualización de resultados**
   - Exportación de queries a CSV para visualización en Tableau / Looker Studio.  
   - Gráficos de crecimiento, cohortes y comparativas de rendimiento por canal.

---

## 📊 Ejemplos de consultas clave

```sql
-- 1️⃣ Clientes activos mensuales
SELECT
    DATE_TRUNC('month', activity_date) AS month,
    COUNT(DISTINCT user_id) AS active_users
FROM user_activity
GROUP BY month
ORDER BY month;

-- 2️⃣ Tasa de conversión por canal
SELECT
    traffic_source,
    COUNT(DISTINCT user_id) FILTER (WHERE status = 'purchase') * 100.0 /
    COUNT(DISTINCT user_id) AS conversion_rate
FROM users
GROUP BY traffic_source
ORDER BY conversion_rate DESC;

-- 3️⃣ LTV promedio
SELECT
    user_id,
    SUM(revenue) AS total_revenue
FROM orders
GROUP BY user_id;
