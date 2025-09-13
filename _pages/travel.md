---
layout: page
title: Travel Map
description: Countries I've visited and lived in
permalink: /travel/
---

<div class="travel-container">
  <div class="map-legend">
    <h3>Legend</h3>
    <div class="legend-item">
      <span class="legend-color visited"></span>
      <span>Visited</span>
    </div>
    <div class="legend-item">
      <span class="legend-color lived"></span>
      <span>Lived In</span>
    </div>
  </div>
  
  <div id="world-map"></div>
  
  <div class="travel-stats">
    <div class="stat">
      <span class="stat-number" id="visited-count">0</span>
      <span class="stat-label">Countries Visited</span>
    </div>
    <div class="stat">
      <span class="stat-number" id="lived-count">0</span>
      <span class="stat-label">Countries Lived In</span>
    </div>
  </div>
</div>

<!-- Leaflet CSS -->
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />

<!-- Leaflet JavaScript -->
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>

<style>
.travel-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

#world-map {
  height: 600px;
  width: 100%;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  margin: 20px 0;
}

.map-legend {
  background: white;
  padding: 15px;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.map-legend h3 {
  margin: 0 0 10px 0;
  font-size: 16px;
  font-weight: 600;
  color: #333;
}

.legend-item {
  display: flex;
  align-items: center;
  margin-bottom: 8px;
}

.legend-item span:last-child {
  color: #333;
  font-weight: 500;
}

.legend-color {
  width: 20px;
  height: 20px;
  border-radius: 4px;
  margin-right: 10px;
  border: 1px solid #ddd;
}

.legend-color.visited {
  background-color: #4CAF50;
}

.legend-color.lived {
  background-color: #2196F3;
}

.travel-stats {
  display: flex;
  justify-content: center;
  gap: 40px;
  margin-top: 20px;
}

.stat {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 2.5em;
  font-weight: bold;
  color: #333;
}

.stat-label {
  font-size: 0.9em;
  color: #666;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

@media (max-width: 768px) {
  #world-map {
    height: 400px;
  }
  
  .travel-stats {
    flex-direction: column;
    gap: 20px;
  }
}

/* Popup styling for darker text */
.leaflet-popup-content {
  color: #333 !important;
  font-weight: 500;
}

.leaflet-popup-content strong {
  color: #000 !important;
  font-weight: 700;
}
</style>

<script>
// Countries data
const visitedCountries = [
  'Switzerland', 'Germany', 'France', 'Italy', 'Austria', 'Spain', 'Portugal',
  'England', 'Norway', 'Turkey', 'Albania', 'Liechtenstein', 'Vatican', 'Czech Republic',
  'Hungary', 'Poland', 'Romania', 'Greece', 'Croatia', 'Morocco', 'USA', 'Canada', 'Mexico',
  'Argentina', 'Chile', 'China', 'Laos', 'Taiwan', 'Vietnam', 'Thailand',
  'Malaysia', 'Singapore', 'Indonesia', 'Denmark'
];

const livedCountries = ['Switzerland', 'Canada', 'Singapore'];

// Initialize map
const map = L.map('world-map').setView([20, 0], 2);

// Add OpenStreetMap tiles
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
  attribution: '© OpenStreetMap contributors'
}).addTo(map);

// Function to get country color based on status
function getCountryColor(countryName) {
  if (livedCountries.includes(countryName)) {
    return '#2196F3'; // Blue for lived in
  } else if (visitedCountries.includes(countryName)) {
    return '#4CAF50'; // Green for visited
  }
  return '#f0f0f0'; // Light gray for not visited
}

// Function to get country opacity
function getCountryOpacity(countryName) {
  if (visitedCountries.includes(countryName)) {
    return 0.7;
  }
  return 0.3;
}

// Load world countries GeoJSON
fetch('https://raw.githubusercontent.com/holtzy/D3-graph-gallery/master/DATA/world.geojson')
  .then(response => response.json())
  .then(data => {
    L.geoJSON(data, {
      style: function(feature) {
        const countryName = feature.properties.name;
        return {
          fillColor: getCountryColor(countryName),
          weight: 1,
          opacity: 1,
          color: '#666',
          fillOpacity: getCountryOpacity(countryName)
        };
      },
      onEachFeature: function(feature, layer) {
        const countryName = feature.properties.name;
        let popupContent = `<strong>${countryName}</strong><br>`;
        
        if (livedCountries.includes(countryName)) {
          popupContent += '🏠 I have lived here';
        } else if (visitedCountries.includes(countryName)) {
          popupContent += '✈️ Already visited ! ';
        } else {
          popupContent += 'Not visited yet';
        }
        
        layer.bindPopup(popupContent);
        
        // Add hover effect
        layer.on('mouseover', function() {
          this.setStyle({
            weight: 3,
            fillOpacity: 1,
            color: '#333'
          });
        });
        
        layer.on('mouseout', function() {
          this.setStyle({
            weight: 1,
            fillOpacity: getCountryOpacity(countryName),
            color: '#666'
          });
        });
      }
    }).addTo(map);
    
    // Update statistics
    document.getElementById('visited-count').textContent = visitedCountries.length;
    document.getElementById('lived-count').textContent = livedCountries.length;
  })
  .catch(error => {
    console.error('Error loading map data:', error);
    document.getElementById('world-map').innerHTML = 
      '<div style="display: flex; align-items: center; justify-content: center; height: 100%; color: #666;">Error loading map data</div>';
  });
</script>
