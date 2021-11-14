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
    result: 0,
  },
  created() {
    const { resultDate, imgUrl } = this.result;
    this.resultDate = resultDate;
    this.imgUrl = imgUrl;
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
    /*  cosumeApi() {
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
    }, */
  },
};
</script>
<style scoped>
img.result-imagery {
  border: 1px solid #dee2e6;
}
</style>
