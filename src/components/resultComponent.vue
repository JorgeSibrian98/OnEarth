<template>
  <!-- Col result -->
  <b-col
    cols="4"
    sm="4"
    md="4"
    lg="4"
    xl="4"
    class="result-col no-gutters-col"
    v-show="gotResult"
  >
    <img
      v-if="imgUrl"
      :src="imgUrl"
      class="img-fluid result-imagery"
      alt="Result image"
    />
    <img
      v-else
      src="../assets/default-not-available-image.png"
      class="img-fluid result-imagery"
      alt="image not available"
    />
    <div class="lon-lat-tile-div" v-if="tileNumber === 5">
      <label style="color: red">{{ lon }}, {{ lat }}</label>
    </div>
    <!--  <div class="result-text mt-2">
      <b-row>
        <b-col class="date-result d-flex align-items-center">
          <strong>{{ resultDate }}</strong>
        </b-col>
      </b-row>
    </div> -->
  </b-col>
  <!--  -->
</template>

<script>
export default {
  props: {
    lon: 0,
    lat: 0,
    result: 0,
    tileNumber: 0,
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
  methods: {},
};
</script>
<style scoped>
img.result-imagery {
  border: 1px solid #dee2e6;
}

.no-gutters-col {
  padding-right: 0px;
  padding-left: 0px;
}

.lon-lat-tile-div {
  position: absolute;
  top: 50%;
  bottom: 50%;
  display: flex;
  justify-content: center;
  z-index: 1;
  overflow: visible;
  width: 100%;
}
</style>
