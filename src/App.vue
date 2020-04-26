<template>
	<div id="app">
		<img alt="Vue logo" src="./assets/logo.png">
		<Dropdown :baseClass="'aaaaaaaa'" :dropdownClass="'asas'" :disabledClass="'asas'"/>
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

