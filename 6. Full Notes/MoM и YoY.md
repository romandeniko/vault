---
created: 2026-08-23T15:19:00
status:
links:
  - "[[SQL]]"
  - "[[Анализ данных в SQL]]"
---
**MoM** (Month-over-Month) — сравнение с предыдущим месяцем. Показывает события прямо сейчас.

**YoY** (Year-over-Year) — сравнение с тем же месяцем год назад. Показывает реальный рост: если вы продаёте лыжи, вам нет смысла сравнивать июль с январём.

#### Вычисление MoM
```sql
WITH monthly AS (
    SELECT
        DATE_TRUNC('month', order_date) AS month,
        SUM(total_amount) AS revenue
    FROM orders
    WHERE status = 'delivered'
        AND order_date >= '2023-12-01' AND order_date < '2024-07-01'
    GROUP BY month
),
with_lag AS (
    SELECT
        month,
        revenue,
        LAG(revenue, 1) OVER (ORDER BY month) AS prev_revenue
    FROM monthly
)
SELECT
    month,
    revenue,
    prev_revenue,
    ROUND(
        ((revenue - prev_revenue) / NULLIF(prev_revenue, 0)) * 100,
        1
    ) AS mom_growth_pct
FROM with_lag
WHERE month >= '2024-01-01'
ORDER BY month;
```

#### Вычисление YoY
```sql
WITH monthly AS (
    SELECT
        DATE_TRUNC('month', order_date) AS month,
        SUM(total_amount) AS revenue
    FROM orders
    WHERE status = 'delivered'
        -- Загружаем данные с запасом в 1 год
        AND order_date >= '2023-01-01' AND order_date < '2024-07-01'
    GROUP BY month
),
with_lag AS (
    SELECT
        month,
        revenue,
        LAG(revenue, 1) OVER (ORDER BY month) AS prev_month,
        LAG(revenue, 12) OVER (ORDER BY month) AS prev_year
    FROM monthly
)
SELECT
    month,
    revenue,
    ROUND(((revenue - prev_month) / NULLIF(prev_month, 0)) * 100, 1) AS mom_pct,
    ROUND(((revenue - prev_year) / NULLIF(prev_year, 0)) * 100, 1) AS yoy_pct
FROM with_lag
-- А вот тут оставляем только нужный период для графиков
WHERE month >= '2024-01-01'
ORDER BY month;
```





























