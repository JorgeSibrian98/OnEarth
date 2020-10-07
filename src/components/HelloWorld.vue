<template>
  <div class="main-home-container">
    <div class="hero-image-div">
      <img
        class="img-fluid hero-image"
        src="../assets/imagery.png"
        fluid
        alt="Responsive image"
      />
      <div class="container-fluid hero-form-container">
        <b-col cols="6" md="6" lg="5">
          <div class="hero-form">
            <h1>SATELLITAL LANDSAT 8 IMAGES</h1>
            <b-form @submit="onSubmit" @reset="onReset">
              <b-row align-v="end">
                <b-col cols="7">
                  <b-form-group
                    class="main-search"
                    id="lonLat-group"
                    label="Longitud, Latitud:"
                    label-for="input-1"
                  >
                    <b-form-input
                      id="lonLat-input"
                      v-model="lonLat"
                      required
                      placeholder="38.883030, -77.016190"
                    ></b-form-input>
                  </b-form-group>
                </b-col>
                <b-col cols="5">
                  <b-button class="large" variant="primary">Find</b-button>
                </b-col>
              </b-row>
            </b-form>
          </div>
        </b-col>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data: {
    lonLat: "",
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped >
.main-home-container {
  max-height: auto;
}

.hero-image {
  height: 0.5%;
  mix-blend-mode: overlay;
}

.hero-image-div {
  max-height: 720px;
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.75);
}

.hero-form-container {
  position: absolute;
  top: 35%;
  color: white;
}

.main-search {
  margin-bottom: 0;
}
</style>
