<template>
  <div id="container">
    <div id="mapContainer"></div>
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";

export default {
  name: "Map",
  data() {
    return {
      center: [-0.789275,113.921327],
      zoom: 5,
      map: null,
    };
  },
  methods: {
    setupLeafletMap () {
      this.map = L.map("mapContainer").setView(this.center, this.zoom);
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(this.map)

      var sld = `
      <?xml version="1.0" encoding="ISO-8859-1"?>
      <StyledLayerDescriptor version="1.0.0"
        xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.0.0/StyledLayerDescriptor.xsd"
        xmlns="http://www.opengis.net/sld" xmlns:ogc="http://www.opengis.net/ogc"
        xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

        <NamedLayer>
          <Name>JawaBarat:jabar3</Name>
          <UserStyle>
            <Title>A cyan polygon style</Title>
            <FeatureTypeStyle>
              <Rule>
                <Title>cyan polygon</Title>
                <PolygonSymbolizer>
                  <Fill>
                    <CssParameter name="fill">#9B5DE5
                    </CssParameter>
                  </Fill>
                  <Stroke>
                    <CssParameter name="stroke">#000000</CssParameter>
                    <CssParameter name="stroke-width">0.5</CssParameter>
                  </Stroke>
                </PolygonSymbolizer>

              </Rule>

            </FeatureTypeStyle>
          </UserStyle>
        </NamedLayer>
      </StyledLayerDescriptor>
      `

      var sld2 = `
      <?xml version="1.0" encoding="ISO-8859-1"?>
      <StyledLayerDescriptor version="1.0.0"
        xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.0.0/StyledLayerDescriptor.xsd"
        xmlns="http://www.opengis.net/sld" xmlns:ogc="http://www.opengis.net/ogc"
        xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

        <NamedLayer>
          <Name>JawaTengah:jateng</Name>
          <UserStyle>
            <Title>A cyan polygon style</Title>
            <FeatureTypeStyle>
              <Rule>
                <Title>cyan polygon</Title>
                <PolygonSymbolizer>
                  <Fill>
                    <CssParameter name="fill">#fee440
                    </CssParameter>
                  </Fill>
                  <Stroke>
                    <CssParameter name="stroke">#000000</CssParameter>
                    <CssParameter name="stroke-width">0.5</CssParameter>
                  </Stroke>
                </PolygonSymbolizer>

              </Rule>

            </FeatureTypeStyle>
          </UserStyle>
        </NamedLayer>
      </StyledLayerDescriptor>
      `

      var sld3 = `
      <?xml version="1.0" encoding="ISO-8859-1"?>
      <StyledLayerDescriptor version="1.0.0"
        xsi:schemaLocation="http://www.opengis.net/sld http://schemas.opengis.net/sld/1.0.0/StyledLayerDescriptor.xsd"
        xmlns="http://www.opengis.net/sld" xmlns:ogc="http://www.opengis.net/ogc"
        xmlns:xlink="http://www.w3.org/1999/xlink" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

        <NamedLayer>
          <Name>JawaTimur:jatim</Name>
          <UserStyle>
            <Title>A cyan polygon style</Title>
            <FeatureTypeStyle>
              <Rule>
                <Title>cyan polygon</Title>
                <PolygonSymbolizer>
                  <Fill>
                    <CssParameter name="fill">#00bbf9
                    </CssParameter>
                  </Fill>
                  <Stroke>
                    <CssParameter name="stroke">#000000</CssParameter>
                    <CssParameter name="stroke-width">0.5</CssParameter>
                  </Stroke>
                </PolygonSymbolizer>

              </Rule>

            </FeatureTypeStyle>
          </UserStyle>
        </NamedLayer>
      </StyledLayerDescriptor>
      `

      L.tileLayer.wms('http://localhost:8080/geoserver/wms', {
          layers: '	JawaBarat:jabar3',
          transparent: true,
          format: 'image/png',
          sld_body: sld
      }).addTo(this.map);

      L.tileLayer.wms('http://localhost:8080/geoserver/wms', {
          layers: '	JawaTengah:jateng',
          transparent: true,
          format: 'image/png',
          sld_body: sld2
      }).addTo(this.map);

      L.tileLayer.wms('http://localhost:8080/geoserver/wms', {
          layers: '	JawaTimur:jatim',
          transparent: true,
          format: 'image/png',
          sld_body: sld3
      }).addTo(this.map);
    },
  },
  mounted() {
    this.setupLeafletMap();
  },
};
</script>

<style scoped>
#container {
  display: flex;
}
#mapContainer {
  width: 100vw;
  height: 100vh;
}
</style>