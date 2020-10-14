<template>
	<div class="container-fluid search-container pt-2">
		<div class="pt-3">
			<b-col cols="12" sm="12" md="8" lg="6" xl="5">
				<MainForm />
			</b-col>
		</div>

		<b-col class="mt-4">
			<SearchComponent :key="counter" />
		</b-col>
	</div>
</template>

<script>
	// @ is an alias to /src
	import SearchComponent from "@/components/searchComponent.vue";
	import MainForm from "@/components/mainForm.vue";
	export default {
		name: "Search",
		components: {
			SearchComponent,
			MainForm,
		},
		data() {
			return {
				counter: 1,
			};
		},
		watch: {
			$route(to, from) {
				console.log(to.query.lon);
				console.log(from.query.lon);

				if (!(to.query.lon == from.query.lon && to.query.lat == from.query.lat)) {
					console.log("equals");
					this.updateSearch();
				}
			},
		},
		methods: {
			updateSearch() {
				this.counter++;
			},
		},
	};
</script>

<style scoped>
	.date-result {
		display: flex;
		padding-top: 0.4rem;
		padding-bottom: 0.4rem;
	}
</style>
