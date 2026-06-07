# 🧪 A/B Test — Streaming Service Recommendation System

> Анализ эффективности новой рекомендательной системы стриминг-сервиса  
> Инструменты: Python · pandas · scipy · seaborn · matplotlib

---

## 📋 О проекте

A/B тест новой рекомендательной системы стриминг-сервиса.  
Цель — оценить влияние фичи на вовлечённость и монетизацию пользователей.

---

## ❓ Гипотезы

**H₀:** Новая рекомендательная система не влияет на ключевые метрики вовлечённости и монетизации

**H₁:** Новая рекомендательная система улучшает вовлечённость (`add_to_playlist`, `active_days`) и монетизацию (`ARPU`, `Renewal Rate`)

---

## 🗂 Данные

| Файл | Описание |
|------|----------|
| `user_event_data_streaming_mini.csv` | События пользователей: `add_to_playlist`, `purchase_*`, `renew`, `cancel`, `start_premium_trial` |
| `subscription_plans_and_retention.csv` | Планы подписки, цены, retention по периодам (1м / 3м / 6м) |

---

## 👥 Сегментация пользователей

| Сегмент | Описание |
|---------|----------|
| `Paid active` | Платные пользователи с высокой активностью (add_to_playlist ≥ 3) |
| `Paid low engagement` | Платные пользователи с низкой активностью |
| `Trial user` | Пользователи на пробном периоде |
| `Free active` | Бесплатные с высокой активностью |
| `Free low engagement` | Бесплатные с низкой активностью |
| `Churned paid` | Платные, отменившие подписку |

---

## 📊 Метрики

| Метрика | Описание |
|---------|----------|
| **ARPU** | Средняя выручка на пользователя |
| **Conversion Rate** | Доля пользователей, перешедших в платный план |
| **Renewal Rate** | Доля пользователей, продливших подписку |
| **LTV** | Пожизненная ценность (горизонт 1м / 3м / 6м) |
| **Active Days** | Количество уникальных активных дней |
| **add_to_playlist count** | Прокси метрика вовлечённости |

---

## 🔬 Статистические методы

- **t-test Уэлча** — сравнение средних (ARPU, Active Days, LTV)
- **Mann-Whitney U** — для непараметрических распределений
- **Chi-square / Fisher Exact** — для конверсионных метрик
- **Когортный анализ** — retention по неделям первой активности

---

## 📈 Результаты

### Общая выборка
| Метрика | p-value | Вывод |
|---------|---------|-------|
| ARPU | > 0.05 | Нет значимой разницы |
| Conversion Rate | > 0.05 | Нет значимой разницы |
| LTV (1м / 3м / 6м) | > 0.05 | Нет значимой разницы |
| Renewal Rate | > 0.05 | Нет значимой разницы |

### Сегмент активных пользователей (Paid active + Free trial active)
| Метрика | p-value | Вывод |
|---------|---------|-------|
| **Active Days** | **0.0447** | ✅ H₀ отклоняется — снижение в тесте |
| **Active Days (Paid+Trial)** | **0.0500** | ✅ H₀ отклоняется — снижение в тесте |
| add_to_playlist | > 0.05 | Нет значимой разницы |
| ARPU | > 0.05 | Нет значимой разницы |

---

## 🏁 Вывод

> **НЕ РЕЛИЗИМ ❌**

Новая рекомендательная система **снижает вовлечённость наиболее активных пользователей** (p = 0.045) без статистически значимого роста монетизации. Риск потери активной аудитории без прироста выручки делает релиз нецелесообразным.

*Оговорка: в части тестов объём данных мог быть недостаточным для достижения нужной статистической мощности.*

---

## 🛠 Стек

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![SciPy](https://img.shields.io/badge/SciPy-8CAAE6?style=for-the-badge&logo=scipy&logoColor=white)
![Seaborn](https://img.shields.io/badge/Seaborn-4C72B0?style=for-the-badge&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)

---

## 📂 Структура репозитория

```
ab-test-streaming/
├── README.md
├── SOAD_rechenie.ipynb          # Основной ноутбук с анализом
└── data/
    ├── subscription_plans_and_retention.csv
    └── user_event_data_streaming_mini.csv
```
