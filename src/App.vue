<template>
	<div id="app">
		<b-navbar class="border" toggleable="lg" type="light">
			<div class="container-fluid">
				<b-navbar-brand href="#"
					><router-link :to="{ name: 'Home' }"
						>ON EARTH</router-link
					></b-navbar-brand
				>
				<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>
			</div>
		</b-navbar>

		<router-view />
	</div>
</template>

