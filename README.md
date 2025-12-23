# RL_for_financial_time_series_forecasting
# Эксперимент: Reinforcement Learning for Time-Series Forecasting

## Описание эксперимента А
Сравнение 6 конфигураций алгоритма PPO с различными функциями награды и архитектурами политик.

## Конфигурации
1. PPO, FinRL env, FinRL policy
2. PPO, FinRL env, Custom policy
3. PPO, Zhang env, FinRL policy
4. PPO, Zhang env, Custom policy
5. PPO, Custom env, FinRL policy
6. PPO, Custom env, Custom policy

## Параметры
- State space: 313
- Total timesteps: 10000
- Дата эксперимента: 2025-12-23 13:22:07

## Результаты
Лучшая модель по Sharpe Ratio: finrl_finrl
Все результаты сохранены в соответствующих папках.

## Описание эксперимента Б
Сравнение 6 конфигураций алгоритма PPO с различными функциями награды и архитектурами политик.

## Конфигурации
1. PPO, FinRL env, FinRL policy
2. PPO, FinRL env, Custom policy
3. PPO, Zhang env, FinRL policy
4. PPO, Zhang env, Custom policy
5. PPO, Custom env, FinRL policy
6. PPO, Custom env, Custom policy

## Параметры
- State space: 313
- Total timesteps: 50000
- Дата эксперимента: 2025-12-23 14:56:06

## Результаты
Лучшая модель по Sharpe Ratio: zhang_custom
Все результаты сохранены в соответствующих папках.
