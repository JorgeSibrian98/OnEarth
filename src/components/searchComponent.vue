<template>
  <div>
    <!-- Lon lat results label -->
    <h4 class="">Results for: {{ lon }}, {{ lat }}</h4>
    <div class="div-results mt-1">
      <!-- row result -->
      <b-row>
        <ResultComponent
          v-for="(result, index) in results"
          :key="index"
          :lat="lat"
          :lon="lon"
          :result="result"
        >
        </ResultComponent>
      </b-row>
    </div>
  </div>
</template>

<script>
import router from "../router";
import ResultComponent from "../components/resultComponent.vue";
import moment from "moment";
import axios from "axios";

export default {
  components: {
    ResultComponent,
  },
  data() {
    return {
      lon: "",
      lat: "",
      results: [],
    };
  },
  async created() {
    if (this.$route.query.lon) {
      this.lon = this.$route.query.lon;
    }

    if (this.$route.query.lat) {
      this.lat = this.$route.query.lat;
    }
    this.results = await this.getResults();
  },
  methods: {
    getResults: async function () {
      const today = new Date();
      let cantSearches = 9;
      let results = [];
      for (cantSearches; cantSearches >= 0; cantSearches--) {
        let searchDate = moment(today).format("YYYY-MM-DD");
        if (cantSearches !== 0) {
          searchDate = moment(today)
            .subtract(cantSearches, "months")
            .format("YYYY-MM-DD");
        }

        const result = await this.getResult(searchDate);
        results.push(result);
      }
      return results;
    },
    getResult: async function (date) {
      let response;
      const defaultResult = {
        imgUrl: null,
        resultDate: null,
      };

      try {
        const api = "https://api.nasa.gov/planetary/earth/assets";
        const response = await axios.get(api, {
          params: {
            lon: this.lon,
            lat: this.lat,
            date: date,
            dim: 0.15,
            api_key: "T24wEaLeAJ0fUJeBlGvgmcz5msBlolkZtNw19qhu",
          },
        });
        if (response.status === 404) {
          return defaultResult;
        } else if (response.status === 200 && response.data) {
          const { url = null, date = null } = response.data;
          return {
            imgUrl: url,
            resultDate: date,
          };
        }

        return defaultResult;
      } catch (error) {
        return defaultResult;
      }
    },
  },
};
</script>