<template>
	<div id = "cesiumContainer" ></div>
</template>

<script lang="ts">
	import { defineComponent } from 'vue'
	import { Viewer, Ion, OpenStreetMapImageryProvider, ImageryLayer, CesiumTerrainProvider, Cartesian3 } from "cesium";
	
	import "cesium/Build/Cesium/Widgets/widgets.css";

	Ion.defaultAccessToken = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJqdGkiOiJkM2I3YTNiNy0wNjNiLTRmNDEtODFiMy05ODAzOGQ2ZTM0YjkiLCJpZCI6NzExNywiaWF0IjoxNjkwOTIzNDQzfQ.hI_Ri0N2Y3bWNzp7ckE4ho6nr4ZQMDMxFrluGgHSdy4';

	declare global {
		interface Window { CESIUM_BASE_URL: string; }
	}

	window.CESIUM_BASE_URL = 'static/cesium';
	

	export default defineComponent({
		name: 'App',	
		async mounted() {
			
			let baseLayer = new ImageryLayer(new OpenStreetMapImageryProvider({
				url: "https://tile.openstreetmap.org/"
			}), {})

			let viewer = new Viewer("cesiumContainer", {
				baseLayer: baseLayer
			});

			viewer.camera.setView({
				destination: new Cartesian3(1263093.7190924052, 5298125.807220887, 3311788.2669270574),
				orientation: {
					heading: 0.6291314004139439,
					pitch: -0.11972375171111294,
					roll: 6.283092953238719
				}
			});

			var terrainProvider = await CesiumTerrainProvider.fromUrl('static/terrain', {});
			viewer.terrainProvider = terrainProvider;
			viewer.scene.globe.terrainExaggeration = 2;
			
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
