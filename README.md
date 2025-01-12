# Bike Share Station Analysis

## Overview
This project analyzes bike-sharing data from San Francisco's bike share system across three time periods:
- July 2014 (7th-13th)
- January 2015 (5th-11th)
- July 2015 (6th-12th)

The analysis explores usage patterns, popular stations, and network characteristics of the bike-sharing system using R.

## Data Sources
The analysis uses four main datasets:
- Station information (containing details about 70 bike stations)
- Trip data from July 2014
- Trip data from January 2015
- Trip data from July 2015

## Dependencies
The project requires the following R packages:
```R
dplyr      # Data manipulation
ggplot2    # Data visualization
igraph     # Network analysis
```

## Key Features

### 1. Basic Data Analysis
- Station information analysis
- Trip count comparisons across different time periods
- Seasonal pattern identification

### 2. Popular Station Analysis
- Identification of top 5 starting and ending stations for each period
- Visualization of station popularity using bar plots
- Analysis of major transportation hubs (e.g., Caltrain stations)

### 3. Network Analysis
The project includes network analysis of bike stations using graph theory:

```224:235:bike-station-analysis.Rmd
create_focused_graph <- function(trips_data, top_stations) {
  top_station_ids <- unique(c(top_stations$top_start, top_stations$top_end))
  filtered_trips <- trips_data %>%
    filter(start_station_name %in% top_station_ids | end_station_name %in% top_station_ids)
  
  edges <- filtered_trips %>%
    group_by(start_station_name, end_station_name) %>%
    summarise(weight = n(), .groups = "drop")
  
  graph <- graph_from_data_frame(edges, directed = TRUE)
  return(graph)
}
```


### 4. Network Visualization
Custom graph visualization with:
- Node coloring based on degree
- Edge width based on trip frequency
- Fruchterman-Reingold layout for optimal spacing

### 5. Network Metrics
Analysis of various network measures including:
- Node count
- Edge count
- Network density
- Average degree
- Network diameter
- Average path length

## Key Findings
1. Seasonal patterns in bike usage (higher in summer months)
2. Consistent popularity of major transit hubs
3. Evidence of network decentralization over time
4. Changes in usage patterns and system growth

## Usage
1. Ensure all required R packages are installed
2. Run the R Markdown file `bike-station-analysis.Rmd`
3. The analysis will generate visualizations and metrics for all three time periods

## Future Work
Potential areas for further analysis:
- Geographical mapping of stations
- Trip duration analysis
- Investigation of new station additions
- Weather impact analysis

## Author
Peter Vu

## License
This project is available for educational and research purposes. Please refer to the original dataset and package licenses for usage restrictions.