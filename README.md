# Spatial Analysis of Airbnb Prices in Rio de Janeiro

## 📋 About the Project

This project investigates the spatial and structural determinants of Airbnb listing prices in the municipality of Rio de Janeiro. The analysis examines how location (Planning Areas) and accommodation type affect prices, using real listing data and city maps.

## 🎯 Objectives

- Analyze the spatial distribution of Airbnb prices in Rio de Janeiro
- Identify location premiums across Planning Areas (APs)
- Evaluate the impact of room type (entire home, private room, shared room, hotel room) on prices
- Map the geographic concentration of listings across the city

## 🗺️ Data Sources

| Source | Description |
|-------|-----------|
| **Inside Airbnb** | Listings with prices, room type, reviews, and coordinates |
| **brazilmaps (R package)** | Shapefile of the municipality of Rio de Janeiro |
| **Data.Rio** | Official neighborhood boundaries and Planning Areas |

## 📊 Key Findings

1. **Clear spatial hierarchy**: South Zone (AP2) has the highest location premium, followed by Barra/Jacarepaguá (AP4)
2. **Room type matters**: Entire homes have significantly higher prices than shared rooms
3. **Downtown as intermediate benchmark**: AP1 (Centro) serves as the baseline category, with average prices
4. **North Zone (AP3)** has lower prices, reflecting less tourism activity
5. **West Zone (AP5)** is heterogeneous, mixing high-value areas like Recreio with peripheral neighborhoods

## 🛠️ Technologies Used

- **Language**: R 4.x
- **Main packages**:
  - `ggplot2` + `ggridges` → visualizations
  - `dplyr` → data manipulation
  - `sf` → spatial analysis
  - `brazilmaps` → Brazilian maps
  - `viridis` → accessible color palettes

## 🔍 Analysis Steps

### 1. Data Wrangling
- Loading the `listings.csv` dataset
- Converting categorical variables (`neighbourhood_group`, `neighbourhood`, `room_type`)
- Handling missing values (`NA`) in the `price` variable
- Creating spatial geometry with `sf` from latitude and longitude
- Using neighborhood boundaries provided by https://www.data.rio/

### 2. Exploratory Data Analysis
- Descriptive statistics: mean, median, and mode of prices and minimum nights
- Frequency distribution of accommodation types
- Top 10 most frequent, most expensive, and cheapest neighborhoods
- Histograms, density plots, and violin plots for `price` and `minimum_nights`
- Visualizations segmented by room type

### 3. Spatial Analysis and Correlations
- Map of Rio de Janeiro's urban structure (Planning Areas)
- Map of Airbnb listing concentration across the city
- Map of average price by neighborhood
- Overlay of listing points with Planning Area boundaries
- Merging listing data with neighborhood shapefile (spatial left join)

### 4. Statistical Modeling
- Model 1: `log(price) ~ area_plane` — pure location effect
- Model 2: `log(price) ~ area_plane + room_type` — adds room type
- Model 3: `log(price) ~ area_plane + room_type + number_of_reviews_ltm` — reputation control

### 🚧 Next Steps (in development)
- **Spatial Econometrics** methods:
  - Spatial weights matrix (W)
  - Spatial autocorrelation test (Moran's I)
  - SAR (Spatial Autoregressive) and SEM (Spatial Error Model) models
  - Controlling for spatial dependence in residuals

## 📚 References

This project was inspired by the Kaggle notebook:  
[Understand Your Data - Airbnb Reservations](https://www.kaggle.com/code/upadorprofzs/understand-your-data-airbnb-reservations)
