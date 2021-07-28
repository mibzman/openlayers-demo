# vue3-openlayers working notes

ol-map probably isn't it

[https://vue3openlayers.netlify.app/componentsguide/map/#methods](https://vue3openlayers.netlify.app/componentsguide/map/#methods)

I'm looking for an object called 'layer', 'layers', or 'map'

[https://vue3openlayers.netlify.app/componentsguide/layers/vectorlayer/#properties](https://vue3openlayers.netlify.app/componentsguide/layers/vectorlayer/#properties)

vector layer is close

ol-source-vector

[https://vue3openlayers.netlify.app/componentsguide/sources/vector/#format](https://vue3openlayers.netlify.app/componentsguide/sources/vector/#format)

allows loading of some formats from just a url, that's cool

no doc for format:

[https://github.com/MelihAltintas/vue3-openlayers/blob/3fc2a41cbe562b847571b3a9b5311fa2d73ebee7/src/index.js#L18](https://github.com/MelihAltintas/vue3-openlayers/blob/3fc2a41cbe562b847571b3a9b5311fa2d73ebee7/src/index.js#L18)

that's an open layers object

yaasssss

[https://openlayers.org/en/latest/apidoc/module-ol_format_KML-KML.html](https://openlayers.org/en/latest/apidoc/module-ol_format_KML-KML.html)

something like:

```jsx
const format = inject('ol-format');
const KML = new format.KML();
```

from open layers:

```jsx
const vector = new VectorLayer({
  source: new VectorSource({
    url: 'data/kml/2012-02-10.kml',
    format: new KML(),
  }),
});
```

I think we just provide a kml url and it'll just work if you specify the format!!!!!

```jsx
https://<staging>/restaurants/<restaurantID>/delivery/kml
```

from open layers

`data/kml/2012-02-10.kml`

[`https://openlayers.org/en/latest/examples/data/kml/2012-02-10.kml`](https://openlayers.org/en/latest/examples/data/kml/2012-02-10.kml)

# Wrapping up notes

use this repo to implement the map.  look at components/Map.vue
