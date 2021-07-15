##2021 7 15

1. nuxt.config.js

디렉토리 위치(프로젝트 바로 밑.  /C/workspace/project1/nuxt.config.js)
```
 plugins: [
    "~/plugins/naverMap.js"
  ],
```
2. naverMap.js

디렉토리 위치(/C/workspace/project1/plugins/naverMap.js)
```
import Vue from 'vue'
import naver from 'vue-naver-maps';

Vue.use(naver, {
  clientID: '23dumy1d' //네이버에서 받은 클라이언트 아이디
});
```
3. naver_map.vue

디렉토리 위치(/C/workspace/project1/pages/order/popup/naver_map.vue)
```
<script>
export default {
  name: 'naverMap',
  data() {
    return {
      width: 560,
      height: 560,
      info: false,
      marker: null,
      count: 1,
      map: null,
      isCTT: false,
      mapOptions: {
        lat: 37,
        lng: 127,
        zoom: 10,
        zoomControl: true,
        zoomControlOptions: {position: 'TOP_RIGHT'},
        mapTypeControl: true,
      },
      initLayers: ['BACKGROUND', 'BACKGROUND_DETAIL', 'POI_KOREAN', 'TRANSIT', 'ENGLISH', 'CHINESE', 'JAPANESE']
    }
  },
  computed: {},
  methods: {
    onLoad(map) {
      this.map = map;
    },
    onWindowLoad(that) {
    },
    onMarkerClicked(event) {
      this.info = !this.info;
    },
    onMarkerLoaded(vue) {
      this.marker = vue.marker;
    },
    close() {
      this.$parent.closeMap()
      console.log('close map self', this.$parent)
    }
  }
}
</script>
<template>
  <div class="container-fluid pop-wrap" v-if="this.$parent.naverMapVisible">
    <div class="pop-con w400">
      <div class="pop-header">
        <h1>
          <i class="ico-car"></i>
          지도보기
        </h1>
        <button @click="close"><i class="ico-close"></i>닫기</button>
      </div>
      <div class="pop-container">
        <div class="map-box">
          <naver-maps
            :width="this.width"
            :height="this.height"
            :mapOptions="this.mapOptions"
            :initLayers="this.initLayers">
          </naver-maps>
        </div>
      </div>
      <div class="pop-foot-btns">
        <button @click="close" class="pop-btn btn-blue"><i class="ico-save"></i>확인</button>
      </div>
    </div>
  </div>
</template>
```
