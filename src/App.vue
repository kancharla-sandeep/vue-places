<template>
  <div id="app">
    <input ref="autocomplete" 
        placeholder="Search" 
        class="search-location"
        onfocus="value = ''" 
        type="text" />
  </div>
</template>

<script>
export default {
  mounted() {
    this.autocomplete = new google.maps.places.Autocomplete(
      (this.$refs.autocomplete),
      {types: ['geocode']}
    );

    this.autocomplete.addListener('place_changed', () => {
      let place = this.autocomplete.getPlace();
      let ac = place.address_components;
      let lat = place.geometry.location.lat();
      let lon = place.geometry.location.lng();
      let city = ac[0]["short_name"];

      console.log(`The user picked ${city} with the coordinates ${lat}, ${lon}`);
    });
  }
}
</script>

<style>
*, *::after, *::before {
  margin: 0;
  padding: 0;
  box-sizing: inherit;
}

body {
  background-color: #dcdde1;
  color: #2f3640;
  padding: 3rem;
}

.search-location {
  display: block;
  width: 60vw;
  margin: 0 auto;
  margin-top: 5vw;
  font-size: 20px;
  font-weight: 400;
  outline: none;
  height: 30px;
  line-height: 30px;
  text-align: center;
  border-radius: 10px;
}
</style>