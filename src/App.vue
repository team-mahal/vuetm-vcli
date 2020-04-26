<template>
	<div id="app">
		<img alt="Vue logo" src="./assets/logo.png">
		<dropdown :baseClass="'aaaaaaaa'" :dropdownClass="'asas'" :disabledClass="'asas'">
			<p class="text-indigo-900">ssssssssssssssssss</p>
			<p class="text-indigo-900">ssssssssssssssssss</p>
			<p class="text-indigo-900">ssssssssssssssssss</p>
			<p class="text-indigo-900">ssssssssssssssssss</p>
		</dropdown>
	</div>
</template>

<script>
import Dropdown from './components/Dropdown.vue'

export default {
	name: 'App',
	components: {
		Dropdown
	}
}
</script>

<style>
	@tailwind base;

	@tailwind components;

	@tailwind utilities;
</style>

