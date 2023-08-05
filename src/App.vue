<template>
	<div id = "cesiumContainer" ></div>
</template>

<script lang="ts">
	import { defineComponent } from 'vue'
	import { Viewer, Ion, OpenStreetMapImageryProvider, ImageryLayer } from "cesium";
	import "cesium/Build/Cesium/Widgets/widgets.css";

	Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJkM2I3YTNiNy0wNjNiLTRmNDEtODFiMy05ODAzOGQ2ZTM0YjkiLCJpZCI6NzExNywiaWF0IjoxNjkwOTIzNDQzfQ.hI_Ri0N2Y3bWNzp7ckE4ho6nr4ZQMDMxFrluGgHSdy4';

	declare global {
		interface Window { CESIUM_BASE_URL: string; }
	}

	window.CESIUM_BASE_URL = '/node_modules/cesium/Build/Cesium';
	

	export default defineComponent({
		name: 'App',	
		mounted() {
			let baseLayer = new ImageryLayer(new OpenStreetMapImageryProvider({
				url: "https://tile.openstreetmap.org/"
			}), {})

			new Viewer("cesiumContainer", {
				baseLayer: baseLayer
			});

			
		}
	})
</script>

<style>
html,
body,
	#cesiumContainer, #app {
		width: 100%;
		height: 100%;
		margin: 0;
		padding: 0;
		overflow: hidden;
		font-family: sans-serif;
	}
</style>
