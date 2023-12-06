<template>
    <div id="map"></div>
</template>

<script setup>
import * as Cesium from 'cesium'
import { app } from '../../main'
// let viewer = null
Cesium.Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiI5MzhjNzg5ZC0zY2JlLTRiMzYtYmU4YS02OGRmMmUyNTVhYmMiLCJpZCI6MTc4MzQ4LCJpYXQiOjE3MDAwMTIwODB9.nqxwRlQvcw3eppW5CuRJ2NrnWQAaYtnKbOizCDj_nqg'
const layer = new Cesium.UrlTemplateImageryProvider({
    url: "http://webrd02.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=8&x={x}&y={y}&z={z}",
    minimumLevel: 4,
    maximumLevel: 18,
});
const esri = new Cesium.ArcGisMapServerImageryProvider({
    url: "https://services.arcgisonline.com/ArcGIS/rest/services/World_Imagery/MapServer"
});
onMounted(() => {

    const viewer = new Cesium.Viewer('map', {
        baseLayerPicker: false, //是否显示图层选择控件
        imageryProvider: esri,
        infoBox: false,
        animation: false, //是否显示动画控件
        timeline: false, //是否显示时间轴控件
        fullscreenButton: false, //是否显示全屏按钮
        geocoder: false, //是否显示搜索按钮
        homeButton: false, //是否显示主⻚按钮
        navigationHelpButton: false,//是否显示帮助提示按钮
        sceneModePicker: false//是否显示投影⽅式按钮
    })
    app.provide('$viewer', viewer)
})

</script>

<style lang="scss">
.cesium-viewer-bottom {
    display: none;
}
</style>

<style lang="scss" scope>
#map {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
}
</style>