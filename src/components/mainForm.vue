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
            :state="isLonLatValid"
            placeholder="-77.016190, 38.883030"
          ></b-form-input>
          <b-form-invalid-feedback :state="isLonLatValid">
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
const lonLatRegex = new RegExp(
  "((\\-?|\\+?)?\\d+(\\.\\d{0,6})?),\\s*((\\-?|\\+?)?\\d+(\\.\\d{0,6})?)"
);
export default {
  name: "MainForm",
  data() {
    return {
      lonLat: "",
      msgLonLat: "",
      isLonLatValid: null,
      lonLatFocus: null,
    };
  },
  methods: {
    submit: function (event) {
      event.preventDefault();
      if (this.isFormValid()) {
        let arr = this.lonLat.split(",", 2);

        this.$router
          .push({
            path: "Search",
            query: { lon: parseFloat(arr[0]), lat: parseFloat(arr[1]) },
          })
          .catch(() => {});
      }
    },

    isLonLatEmpty: function () {
      if (!this.lonLat || this.lonLat.length < 1 || this.lonLat == "") {
        return true;
      }
      return false;
    },
    isLonLatValidString: function () {
      if (!lonLatRegex.test(this.lonLat)) {
        return false;
      }
      return true;
    },
    canConvertLongLatToFloat: function () {
      if (!this.isLonLatEmpty() && this.isLonLatValidString()) {
        let arr = this.lonLat.split(",", 2);
        if (!parseFloat(arr[0]) || !parseFloat(arr[1])) {
          return false;
        }
        return true;
      }
    },
    validateLongLat: function () {
      const emptyErrorMessage = "Please insert a longitude and latitude value";
      const invalidLonLatMessage =
        "Not a valid format for longitude or latitude. Try a number format like: -99.99 or 99.99";
      const invalidLonLatConversionMessage =
        "Invalid value for longitude or latitude. Try a number format like: -99.99 or 99.99";

      if (this.isLonLatEmpty()) {
        this.isLonLatValid = false;
        this.msgLonLat = emptyErrorMessage;
        return false;
      }

      if (!this.isLonLatValidString()) {
        this.isLonLatValid = false;
        this.msgLonLat = invalidLonLatMessage;
        return false;
      }

      if (!this.canConvertLongLatToFloat()) {
        this.isLonLatValid = false;
        this.msgLonLat = invalidLonLatConversionMessage;
        return false;
      }

      this.isLonLatValid = true;
      this.msgLonLat = "";
      return true;
    },
    isFormValid: function () {
      if (this.validateLongLat()) {
        return true;
      }
      return false;
    },
  },
};
</script>

<style scoped>
.main-search {
  margin-bottom: 0;
}

.b-button-submit {
  margin-top: 2rem;
}

.invalid-feedback {
  color: #eb7d86;
  font-size: 1rem;
  font-weight: 600;
}
</style>
