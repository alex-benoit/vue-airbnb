<template>
  <div class="flat" v-on:click="handleClick">
    <div class="flat-picture" v-bind:style="{ backgroundImage: `url(${flatInfo.imageUrl})` }"></div>
    <div class="flat-title">
      {{ title }}
    </div>
  </div>
</template>

<script>
export default {
  computed: {
    title: function() {
      return `${this.flatInfo.price} ${this.flatInfo.priceCurrency} - ${this.flatInfo.name}`
    }
  },
  props: ['flatInfo'],
  methods: {
    handleClick: function(){
      this.$emit('selectedFlatChanged', this.flatInfo)
    }
  }
}
</script>

<style scoped>
.flat {
  flex-basis: calc(50% - 20px);
  margin: 10px;
  cursor: pointer;
}

.flat:hover {
  opacity: 0.8;
}

.flat-picture {
  height: 200px;
  background-size: cover;
  background-position: center;
}

.flat-title {
  margin-top: 10px;
  font-weight: bold;
}
</style>
