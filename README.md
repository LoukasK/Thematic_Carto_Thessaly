# Multi-Layer Interactive Cartography Viewer

A comprehensive web-based cartographic application demonstrating six different thematic mapping techniques simultaneously using MapLibre GL JS. Features multiple classification methods, interactive layer controls, and extensive student documentation.

## Features

### Six Visualization Layers

1. **Choropleth Map** - Population density by administrative area
   - Equal Interval, Quantile, Jenks Natural Breaks, or Custom classification
   - 3-7 class options
   - Adjustable opacity

2. **Dasymmetric Map** - Population density refined by land cover zones
   - Same classification options as choropleth
   - Higher spatial accuracy than traditional choropleth
   - Independent opacity control

3. **Proportional Symbols** - Graduated circles sized by total population
   - Flannery scaling (exponent 0.57) for perceptual accuracy
   - Adjustable maximum radius (20-200px)
   - Sorted rendering (largest first) for visibility
   - Default start: 100px radius

4. **Isopleths (Contours)** - Lines of equal population potential
   - Primary (thick) and secondary (thin) contours
   - Shows zones of demographic influence
   - Variable line width by importance

5. **Dot Density Map** - One dot per X people
   - Adjustable dot size (0.5-6px)
   - Pattern reveals distribution at fine scale
   - Independent opacity control

6. **Municipal Boundaries** - Administrative division outlines
   - Geographic context layer
   - Adjustable opacity
   - Works as reference for other layers

### Interactive Controls

- **Layer Toggle**: Individual on/off controls for each layer
- **Classification Methods**: 
  - Equal Interval (uniform class widths)
  - Quantiles (equal feature counts)
  - Natural Breaks / Jenks (optimized variance)
  - Custom intervals (user-defined breaks)
- **Dynamic Legend**: Automatically updates based on active layers and settings
- **Basemap Switching**: Light/Dark CartoDB basemaps
- **Resizable Legend**: Drag corner to resize legend panel

## Technical Implementation

### Core Technologies
- **MapLibre GL JS 3.6.2**: Vector tile mapping library
- **JavaScript (ES6)**: Pure vanilla JS, no framework dependencies
- **GeoJSON**: Six separate data layers
- **SVG**: Dynamic legend rendering

### Classification Algorithms

**Equal Interval**
```javascript
// Divides data range into equal-sized bins
// PROS: Easy to understand, consistent intervals
// CONS: May result in empty or sparse classes
```

**Quantile**
```javascript
// Each class contains equal number of features
// PROS: Every class well-represented
// CONS: Can group dissimilar values together
```

**Jenks Natural Breaks**
```javascript
// Minimizes within-class variance
// PROS: Statistically optimal, finds natural groupings
// CONS: More complex, harder to explain
```

**Custom**
```javascript
// User-defined break values
// PROS: Domain knowledge applied, meaningful thresholds
// CONS: Requires data understanding
```

### Data Requirements

All layers expect GeoJSON files in `data/` folder:

| Layer | Geometry | Required Field | Example |
|-------|----------|----------------|---------|
| Choropleth | Polygon | `POPDENS` | Population density (people/km²) |
| Dasymmetric | Polygon | `DENS_COVER` | Density by land cover zone |
| Proportional | Point | `POPMUN` | Total population |
| Contours | LineString | `ID` | Contour importance (1=primary) |
| Dots | Point | (none) | One point per N people |
| Boundaries | Polygon | (none) | Administrative borders |

**Coordinate System**: WGS84 (EPSG:4326)

## Student Customization

### 🌍 Mandatory Changes

**1. Map Settings** (Lines ~351-355)
```javascript
center: [22.4, 39.6],  // Your study area coordinates
zoom: 8                 // Appropriate zoom level
```

**2. Data Configuration** (Lines ~370-410)
```javascript
url: 'data/your_file.geojson',    // Update all 6 file paths
dataField: 'YOUR_COLUMN_NAME'      // Update field names to match your data
```

**3. Color Schemes** (Lines ~437-462)
```javascript
// 12 color examples provided:
// Red, Blue, Green, Orange, Purple, Magenta, 
// Yellow, Cyan, Gray, Brown, Pink, Teal
```

**4. Legend Title** (Lines ~996-1008)
```javascript
// Map title, data source, author, institution
```

### 🗺️ Optional Styling

- Proportional symbol colors (fill and stroke)
- Contour line colors and widths
- Dot colors and "people per dot" ratio
- Boundary line appearance
- Legend circle sizes (Lines ~1068-1075)

### Cross-Reference System

Every color/setting includes line number references to related locations:
```javascript
// Example:
'circle-color': 'red',  // 🗺️ Change here (also update legend Line ~1107)
```

## File Structure
```
├── index.html                              # Main application
├── data/
│   ├── dimoi_popdens_WGS.geojson          # Choropleth data
│   ├── dimoi_popdens_cover_WGS.geojson    # Dasymmetric data
│   ├── dimoi_poi_pop_WGS.geojson          # Proportional symbols
│   ├── pop_contours_200k_WGS.geojson      # Contour lines
│   ├── pop_dots_300_WGS.geojson           # Dot density points
│   └── dimoi_oria_WGS.geojson             # Boundaries
```

## Usage

1. **Prepare Data**: Ensure all 6 GeoJSON files are in `data/` folder
2. **Update Configuration**: Modify file paths and field names (Lines ~370-410)
3. **Set Map Extent**: Configure center and zoom (Lines ~351-355)
4. **Customize Colors**: Choose color schemes for choropleth/dasymmetric (Lines ~437-462)
5. **Update Credits**: Add your name and institution (Lines ~996-1008)
6. Open `index.html` in web browser

## Key Features for Education

### Automatic Legend Generation
- Legend updates dynamically as layers are toggled on/off
- Colors automatically synchronized between map and legend
- No manual legend editing required

### Classification Comparison
Students can compare four classification methods on the same data:
- Toggle between methods to see visual differences
- Understand how method choice affects interpretation
- Learn appropriate use cases for each method

### Multi-Representation Analysis
View same population data through six different cartographic lenses:
- Areal (choropleth, dasymmetric)
- Point (proportional symbols, dots)
- Linear (contours)
- Reference (boundaries)

### Code Documentation
- **1000+ lines** of educational comments
- **Line number cross-references** throughout
- **Troubleshooting section** with common issues
- **Step-by-step customization guide**
- **Hex color reference** with 12 examples

## Cartographic Concepts Demonstrated

1. **Data Classification**: Multiple methods for grouping continuous data
2. **Visual Variables**: Size (circles), color (choropleth), texture (dots)
3. **Dasymetric Mapping**: Ancillary data improves accuracy over choropleth
4. **Flannery Scaling**: Perceptual correction for proportional symbols
5. **Isopleth Mapping**: Smooth interpolation of point data
6. **Dot Density**: One-to-many representation technique
7. **Layer Ordering**: Rendering sequence affects perception
8. **Color Theory**: Sequential schemes for quantitative data

## Browser Compatibility

- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- WebGL required

## Educational Context

Designed for cartography curriculum covering:
- Thematic mapping techniques
- Statistical classification methods
- Multi-layer cartographic composition
- Web cartography and GIS
- Data-driven visualization
- Perceptual principles in cartography

Perfect for undergraduate/graduate courses in:
- Thematic Cartography
- Geographic Visualization
- WebGIS Development
- Spatial Data Analysis

## Performance Considerations
- Keep GeoJSON files under 5MB each for optimal performance
- Dot density layer can be performance-intensive with >50,000 points
- Consider simplifying geometries for web use (e.g., using Mapshaper)
- Feature sorting adds minimal overhead (<100ms for typical datasets)


## Credits
Population data: Hellenic Statistical Authority (ELSTAT)
Educational materials developed for the Cartography Laboratory, School of Rural, Surveying & Geoinformatics Engineering, National Technical University of Athens (NTUA).

## References
- Flannery, J.J. (1971). "The Relative Effectiveness of Some Common Graduated Point Symbols in the Presentation of Quantitative Data". *Cartographica* 8(2): 96-109.
- ColorBrewer 2.0: https://colorbrewer2.org/
- MapLibre GL JS: https://maplibre.org/

## License
Educational use. Attribution required when adapting for other projects.
