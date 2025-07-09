# 🚗 Dynamic Pricing for Urban Parking Lots

## 📌 Project Overview

This project implements a smart, real-time dynamic pricing engine for 14 urban parking spaces using real-world-inspired data. It simulates a pricing strategy that adjusts based on demand, traffic, queue length, vehicle type, and special day indicators. The goal is to optimize parking lot utilization by preventing both overcrowding and underutilization.

The system ingests streaming data using **Pathway**, computes prices using three pricing models, and provides real-time visualizations using **Bokeh** and **Google Colab**.

---

## 🧰 Tech Stack

| Layer                   | Technology                                    |
| ----------------------- | --------------------------------------------- |
| Data Processing         | `pandas`, `numpy`                             |
| Streaming Engine        | `pathway`                                     |
| Visualization           | `bokeh`, `ipywidgets`, `Google Colab`         |
| Dashboarding (optional) | `panel` (deprecated in Colab)                 |
| Version Control         | `Git`, `GitHub`                               |
| Documentation           | `README.md`, architecture diagram via Mermaid |

---

## 📊 Pricing Models Implemented

### Model 1: Linear Occupancy-Based Model

```math
Price_{t+1} = Price_t + \alpha \cdot \left(\frac{Occupancy}{Capacity}\right)
```

* Price increases linearly with occupancy.
* Simple, baseline reference model.

### Model 2: Demand-Based Pricing

```math
Demand = 0.5 \cdot OccupancyRate + 0.3 \cdot QueueLength - 0.2 \cdot Traffic + 0.4 \cdot IsSpecialDay + 1.0 \cdot VehicleWeight
Price = BasePrice \cdot (1 + 0.2 \cdot NormalizedDemand)
```

* Incorporates multiple real-world signals.
* Dynamically adjusts price based on total demand signal.

### Model 3: Competitive Pricing

* If the lot is full, decrease price to reroute traffic.
* If nearby lots are expensive, increase price moderately.
* Simulates real-world market competition.

---

## 🏗️ Architecture Diagram
![Untitled diagram _ Mermaid Chart-2025-07-09-175424](https://github.com/user-attachments/assets/13855065-8b91-4bc6-b6e3-51ce96128082)


---

## 🔄 Project Workflow

1. **Data Preprocessing**:

   * Combine timestamp columns
   * Handle missing or invalid values
   * Normalize numeric and categorical fields

2. **Real-Time Simulation**:

   * Use `pathway.demo.replay_csv()` to simulate streaming
   * Cast all fields to Pathway-safe types

3. **Pricing Logic**:

   * Implement `model_1`, `model_2`, and `model_3` using `@pw.udf`
   * Store and output results in a live stream CSV

4. **Visualization**:

   * Load CSV into pandas
   * Use `bokeh` + `ipywidgets` to build interactive dashboard
   * User can select parking lot and see all 3 pricing models in real time

---

## 📂 File Structure

```
.
├── dataset.csv                # Raw input data
├── parking_stream_final.csv  # Cleaned data for streaming
├── output_stream.csv         # Result with pricing models
├── DynamicPricing.ipynb      # Main Colab notebook
├── README.md                 # Project documentation
```

---

## 🙌 Acknowledgements

* [Pathway](https://pathway.com)
* [Bokeh](https://bokeh.org)
* [Panel](https://panel.holoviz.org) for dashboard prototype
* Dataset provided as part of Summer Analytics 2025
