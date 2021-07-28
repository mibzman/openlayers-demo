<template>
<input type="checkbox" id="fullscreencontrol" v-model="fullscreencontrol">
<label for="fullscreencontrol">fullscreencontrol</label>
<input type="checkbox" id="attribution" v-model="attributioncontrol">
<label for="attribution">attributioncontrol</label>
<input type="checkbox" id="zoom" v-model="zoomcontrol">
<label for="zoom">zoomcontrol</label>
<input type="checkbox" id="zoomtoextent" v-model="zoomtoextentcontrol">
<label for="zoomtoextent">zoomtoextentcontrol</label>
<input type="checkbox" id="zoomslider" v-model="zoomslidercontrol">
<label for="zoomslider">zoomslidercontrol</label>
<input type="checkbox" id="scaleline" v-model="scalelinecontrol">
<label for="scaleline">scalelinecontrol</label>
<input type="checkbox" id="overviewmap" v-model="overviewmapcontrol">
<label for="overviewmap">overviewmapcontrol</label>
<input type="checkbox" id="mousepositioncontrol" v-model="mousepositioncontrol">
<label for="mousepositioncontrol">mousepositioncontrol</label>
<input type="checkbox" id="rotatecontrol" v-model="rotatecontrol">
<label for="rotatecontrol">rotatecontrol</label>

<ol-map ref="map" :loadTilesWhileAnimating="true" :loadTilesWhileInteracting="true" style="height:400px">

    <ol-view ref="view" :center="center" :rotation="rotation" :zoom="zoom" :projection="projection" />

    <ol-fullscreen-control v-if="fullscreencontrol" />
    <ol-mouseposition-control v-if="mousepositioncontrol" />
    <ol-attribution-control v-if="attributioncontrol" />

    <ol-overviewmap-control v-if="overviewmapcontrol">
        <ol-tile-layer>
            <ol-source-osm />
        </ol-tile-layer>
    </ol-overviewmap-control>

    <ol-scaleline-control v-if="scalelinecontrol" />
    <ol-rotate-control v-if="rotatecontrol" />
    <ol-zoom-control v-if="zoomcontrol" />
    <ol-zoomslider-control v-if="zoomslidercontrol" />
    <ol-zoomtoextent-control v-if="zoomtoextentcontrol" :extent="[23.906,42.812,46.934,34.597]" tipLabel="Fit to Turkey" />

    <ol-tile-layer>
        <ol-source-osm />
    </ol-tile-layer>

    <ol-vector-layer>
        <ol-source-vector :url="url" :format="kml">

        </ol-source-vector>

    </ol-vector-layer>

</ol-map>
</template>

<script>

// https://vue3openlayers.netlify.app/componentsguide/sources/vector/#usage
// there's probably ways to color those circles something other than white


import { ref, inject } from "vue";
export default {
  setup() {
    const center = ref([-81.51214560283877, 41.07716717533248]);
    const projection = ref("EPSG:4326");
    const zoom = ref(10);
    const rotation = ref(0);

    const url = ref("https://<staging>/api/restaurants/<restaurantID>/delivery/kml");
    

    const format = inject('ol-format');
    console.log(format)
    const kml = new format.KML();


    return {
      center,
      projection,
      zoom,
      rotation,
      kml,
      url,
    };
  },
  data() {
    return {
      fullscreencontrol: true,
      attributioncontrol: true,
      zoomcontrol: true,
      zoomslidercontrol: true,
      zoomtoextentcontrol: true,
      scalelinecontrol: true,
      overviewmapcontrol: true,
      mousepositioncontrol: true,
      rotatecontrol: true,
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
