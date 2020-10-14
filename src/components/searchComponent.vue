<template>
	<div>
		<!-- Lon lat results label -->
		<h4 class="">Results for: {{ lon }}, {{ lat }}</h4>
		<div class="div-results mt-1">
			<!-- row result -->
			<b-row>
				<ResultComponent v-for="n in 9" :key="n" :lat="lat" :lon="lon" :n="n">
				</ResultComponent>
			</b-row>
		</div>
	</div>
</template>

<script>
	import router from "../router";
	import ResultComponent from "../components/resultComponent.vue";

	export default {
		components: {
			ResultComponent,
		},
		data() {
			return {
				lon: "",
				lat: "",
			};
		},
		created() {
			if (this.$route.query.lon) {
				this.lon = this.$route.query.lon;
			}

			if (this.$route.query.lat) {
				this.lat = this.$route.query.lat;
			}
		},
	};
</script>