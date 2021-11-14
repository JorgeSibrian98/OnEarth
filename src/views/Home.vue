<template>
  <div class="home">
    <div class="main-home-container">
      <div class="hero-image-div">
        <!-- images -->
        <!-- desktop and tablet image  -->
        <img
          class="img-fluid hero-image d-none d-sm-none d-md-block"
          src="../assets/imagery.png"
          fluid
          alt="Responsive image"
        />
        <!-- desktop and tablet image  -->
        <!-- Mobile devices image  -->
        <img
          class="img-fluid hero-image d-block d-sm-block d-md-none"
          src="../assets/imagery-9-16.png"
          fluid
          alt="Responsive image"
        />
        <!-- Mobile devices image  -->
        <!-- images -->
        <!-- form  -->
        <div class="container-fluid hero-form-container">
          <b-col cols="12" sm="8" md="7" lg="6" xl="5">
            <div class="hero-form">
              <h1>SATELLITAL LANDSAT 8 IMAGES</h1>
              <!-- form component-->
              <MainForm />
            </div>
          </b-col>
        </div>
        <!-- form -->
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import MainForm from "@/components/mainForm.vue";

export default {
  name: "Home",
  components: {
    MainForm,
  },
};
</script>

<style scoped>
.main-home-container {
  max-height: auto;
}

.hero-image {
  height: auto;
  mix-blend-mode: overlay;
}

.hero-image-div {
  max-height: 720px;
  overflow: hidden;
  background-color: rgba(0, 0, 0, 0.75);
}

.hero-form-container {
  position: absolute;
  color: white;
}
</style>
