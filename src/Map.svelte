<script>
 import { onMount } from 'svelte';
 import leaflet from 'leaflet';
 import { mapOptions, selectedAreaID, selectedArea } from './store/store.js';
 import { kreise } from './geodata/kreise.js';
 const landKreise = kreise.features;

 let map;
 let basemap;

 function getSelectedAreaID(){
   return $selectedAreaID;
 }


onMount(() => {
		const link = document.createElement('link');
		link.rel = 'stylesheet';
		link.href = 'https://unpkg.com/leaflet@1.5.1/dist/leaflet.css';

		link.onload = () => {
      map = L.map('map', $mapOptions);
      L.control.zoom({position: 'topright'}).addTo(map);

      // basemap = L.tileLayer('https://{s}.basemaps.cartocdn.com/light_all/{z}/{x}/{y}{r}.png', {
      //   attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
      //   subdomains: 'abcd',
      //   maxZoom: 19
      // }).addTo(map);


      // OnEach feature function
      function onEachFeature(feature, layer) {
      if (feature.properties) {
        layer.on('click', function() {
          $selectedAreaID = feature.properties['ID_3'];
          $selectedArea = feature;
          console.log($selectedAreaID);
        })
      
      }
    }

    let kreiseNew = L.geoJSON(kreise, {
        onEachFeature: onEachFeature
    }).addTo(map);

    map.fitBounds(kreiseNew.getBounds());
		};



		document.head.appendChild(link);

		return () => {
			map.remove();
			link.parentNode.removeChild(link);
    };
    
  });



  // // Load geodata dynamically from URL
  // loadGeoData();

  // async function loadGeoData() {
	// 	const res = await fetch(`https://raw.githubusercontent.com/isellsoap/deutschlandGeoJSON/master/4_kreise/4_niedrig.geojson`);
	// 	const data = await res.json()

	// 	if (res.ok) {
  //     $geoData = data;
  //     L.geoJSON($geoData).addTo(map);      
	// 	} else {
	// 		throw new Error(data);
	// 	}
	// }

</script>

<style>
  #map {
      flex: 3;
      background: #fff;
    }
</style>

<div id="map"></div>
