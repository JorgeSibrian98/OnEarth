<template>
	<b-form @submit="submit" novalidate>
		<b-row align-v="start">
			<b-col cols="12" md="7">
				<b-form-group
					class="main-search"
					id="lonLat-group"
					label="Longitude, Latitude:"
					label-for="lonLat-input"
				>
					<b-form-input
						id="lonLat-input"
						v-model="lonLat"
						required
						:state="lonLatValidComputed"
						v-on:focus="FocusLonLat"
						placeholder="-77.016190, 38.883030"
					></b-form-input>
					<b-form-invalid-feedback :state="lonLatValidComputed">
						{{ msgLonLat }}
					</b-form-invalid-feedback>
				</b-form-group>
			</b-col>
			<b-col cols="5">
				<b-button type="submit" class="large b-button-submit" variant="primary"
					>Find</b-button
				>
			</b-col>
		</b-row>
	</b-form>
</template>

<script>
	import router from "../router";
	var lonLatRegex = new RegExp(
		"((\\-?|\\+?)?\\d+(\\.\\d{0,6})?),\\s*((\\-?|\\+?)?\\d+(\\.\\d{0,6})?)"
	);
	export default {
		name: "MainForm",
		data() {
			return {
				lonLat: "",
				msgLonLat: "",
				lonLatFocus: null,
			};
		},

		computed: {
			lonLatValidComputed: function () {
				if (!this.lonLatFocus) {
					return null;
				}

				if (!this.lonLat || this.lonLat.length < 1 || this.lonLat == "") {
					this.msgLonLat = "this can not be empty";
					return false;
				}

				if (!lonLatRegex.test(this.lonLat)) {
					this.msgLonLat = "Not a valid format for longitude or latitude";
					return false;
				}
				if (this.lonLat) {
					var arr = this.lonLat.split(",", 2);
					if (!parseFloat(arr[0]) || !parseFloat(arr[1])) {
						this.msgLonLat = "Not a valid format for longitude or latitude";
						return false;
					}
				}

				this.msgLonLat = "";
				return true;
			},
		},
		methods: {
			submit: function (event) {
				event.preventDefault();
				if (this.lonLatValidComputed) {
					var arr = this.lonLat.split(",", 2);
					//alert("Lon: " + parseFloat(arr[0]) + "Lat: " + parseFloat(arr[1]));
					this.$router
						.push({
							path: "Search",
							query: { lon: parseFloat(arr[0]), lat: parseFloat(arr[1]) },
						})
						.catch(() => {});
				}
			},
			FocusLonLat() {
				this.lonLatFocus = true;
			},
		},
	};
</script>

<style scoped >
	.main-search {
		margin-bottom: 0;
	}

	.b-button-submit {
		margin-top: 2rem;
	}
</style>
