<template>
  <div class="flat-panel" v-if="selectedFlat">
    <div class="flat-info">
      <h3>{{ selectedFlat.name }}</h3>
      <p>{{ selectedFlat.price }} {{ selectedFlat.priceCurrency }} per night</p>
      <button>Book now</button>
    </div>
    <div class="flat-banner" v-bind:style="{ backgroundImage: `url(${selectedFlat.imageUrl})` }"></div>
    <div class="flat-map" v-bind:style="{ backgroundImage: `url(${mapUrl})`}"></div>
  </div>
</template>

<script>
export default {
  props: [ 'selectedFlat' ],
  computed: {
    mapUrl: function(){
      return `http://maps.googleapis.com/maps/api/staticmap?center=${this.selectedFlat.lat},${this.selectedFlat.lng}&zoom=14&size=480x250&markers=${this.selectedFlat.lat},${this.selectedFlat.lng}&key=AIzaSyCP18cD4FwL37eXgcB1MbLNtG9ktbkzdlw`
    }
  }
};
</script>

<style scoped>
.flat-panel {
  margin: 10px;
  background-color: #eee;
  border-radius: 3px;
  padding: 10px;
}

.flat-banner {
  height: 250px;
  background-size: cover;
  background-position: center;
  margin-bottom: 15px;
}

.flat-map {
  height: 250px;
  background-size: cover;
  background-position: center;
}

.flat-info {
  padding: 10px;
  background-color: #ddd;
  margin-bottom: 15px;
}

.flat-info button {
  color: white;
  padding: 8px;
  font-size: 18px;
  cursor: pointer;
  background-color: #FD5C63;
  width: 100%;
}
</style>
