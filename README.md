# Airline Booking Demand Forecasting

Built a weekday-sensitive forecasting model that predicts final airline booking demand from partial, in-progress booking data — **24% more accurate than a naive baseline** (MASE 0.64 vs. 0.84).

MSBA capstone project (BUAN 5201, Seattle University), co-authored with Mukti Maitree Mahjabin.

**Skills demonstrated:** time series feature engineering, model comparison, forecast evaluation (MASE), Python/pandas, translating an analytical result into a business recommendation.

## Problem

Airlines need to predict how many seats will ultimately be booked on a flight well before departure, using only the bookings-to-date. A flight 45 days out with 60 bookings could end up anywhere between 100 and 250 total bookings depending on the day of week and how demand typically builds. The goal was to build a forecasting model that beats a naive "assume it ends up like average" baseline.

## Approach

- Built a **booking curve**: average cumulative bookings by days-prior-to-departure, learned from ~4,700 historical training records
- Developed three models:
  - **Naive** — flat average final demand, ignoring current bookings
  - **Additive** — current bookings + average remaining demand for that many days out
  - **Multiplicative / weekday-sensitive** — same idea, but the booking curve is learned separately per departure weekday, since demand builds differently on a Friday flight vs. a Tuesday flight
- Validated all three models against held-out data using **MASE** (Mean Absolute Scaled Error)

## Results

| Model | MASE |
|---|---|
| Naive (baseline) | 0.84 |
| Weekday-sensitive additive | **0.64** |

The weekday-sensitive additive model outperformed the naive baseline by ~24%, confirming that day-of-week booking patterns are a meaningful signal for near-term demand forecasting — and that a simple, interpretable model can beat "assume average" without needing a black-box approach.

## Repo contents

| File | Description |
|---|---|
| `notebook.ipynb` | Full analysis: model training, weekday-sensitive curve fitting, validation, MASE comparison |
| `data/airline_data_training.csv` | Training data (historical booking curves) |
| `data/airline_data_validation.csv` | Held-out validation data |
| `Airline_Forecasting_Report.docx` | Written report |
| `Airline_Forecasting_Slides.pptx` | Presentation deck |

## Tools

Python, pandas — see `requirements.txt`

## Author

Savgun Kaur ([savscripts](https://github.com/savscripts)) — co-authored with Mukti Maitree Mahjabin
