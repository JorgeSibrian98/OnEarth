<template>
	<!-- Col result -->
	<b-col
		cols="12"
		sm="6"
		md="4"
		lg="4"
		xl="3"
		class="result-col mt-3 mb-3"
		v-show="gotResult"
	>
		<img :src="imgUrl" class="img-fluid result-imagery" alt="Result image" />
		<div class="result-text mt-2">
			<b-row>
				<b-col class="date-result d-flex align-items-center">
					<strong>{{ resultDate }}</strong>
				</b-col>
				<b-col class="d-flex justify-content-end">
					<b-button
						v-on:click="download"
						class="large b-button-download"
						variant="primary"
						>Download</b-button
					>
				</b-col>
			</b-row>
		</div>
	</b-col>
	<!--  -->
</template>

<script>
	import axios from "axios";
	import moment from "moment";
	const Fs = require("fs");
	const Path = require("path");

	export default {
		props: {
			lon: 0,
			lat: 0,
			n: 0,
		},
		created() {
			var today = new Date();
			this.searchDate =
				"" +
				(today.getFullYear() - this.n) +
				"-" +
				today.getMonth() +
				"-" +
				today.getDate();
			this.cosumeApi();
		},
		data() {
			return {
				searchDate: "",
				resultDate: "",
				imgUrl: "",
				gotResult: true,
			};
		},
		methods: {
			cosumeApi() {
				var api = "https://api.nasa.gov/planetary/earth/assets";
				axios
					.get(api, {
						params: {
							lon: this.lon,
							lat: this.lat,
							date: this.searchDate,
							dim: 0.15,
							api_key: "T24wEaLeAJ0fUJeBlGvgmcz5msBlolkZtNw19qhu",
						},
					})
					.then((response) => {
						var apiData = response.data;

						if (apiData.date && apiData.url) {
							this.gotResult = true;
							this.imgUrl = apiData.url;
							this.resultDate = moment(apiData.date).format(
								"MMMM Do YYYY, h:mm:ss a"
							);
						} else {
							this.gotResult = false;
						}

						//console.log(response.data);
					})
					.catch((error) => {
						console.log(error.response.status);
						if (error.response.status == 404) {
							this.gotResult = false;
						}
					});
			},

			download: async function () {
				await axios({
					url: this.imgUrl,
					method: "GET",
					responseType: "blob",
				}).then((response) => {
					var fileURL = window.URL.createObjectURL(new Blob([response.data]));
					var fileLink = document.createElement("a");

					fileLink.href = fileURL;
					fileLink.setAttribute(
						"download",
						"" +
							moment(this.resultDate, "MMMM Do YYYY, h:mm:ss a").format(
								"YYYY-MM-DD, h-mm-ss a"
							) +
							" lon" +
							this.lon +
							" lat" +
							this.lat +
							".png"
					);
					document.body.appendChild(fileLink);

					fileLink.click();
				});
			},
		},
	};
</script>
<style scoped>
	.result-imagery {
		border: 1px solid #dee2e6 !important;
	}
</style>