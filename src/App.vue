<template>
  <div class="container">
    <div class="main">
      <div class="search">
        <input type="text" v-model="query" v-on:input="filterFlats">
      </div>
      <div class="flats">
        <flat v-for='flat in flats' v-bind:flatInfo='flat' v-on:selectedFlatChanged='changedSelectedFlat'></flat>
      </div>
    </div>
    <div class="panel">
      <panel v-bind:selectedFlat="selectedFlat"></panel>
    </div>
  </div>
</template>

<script>
import Flat from './components/flat.vue'
import Panel from './components/panel.vue'

export default {
  data () {
    return {
      query: '',
      allFlats: [],
      flats: [],
      selectedFlat: null
    }
  },
  components: { Flat, Panel },
  mounted: function() {
    this.$http.get('https://raw.githubusercontent.com/lewagon/flats-boilerplate/master/flats.json')
      .then(response => response.json())
      .then(data => {
        this.allFlats = data;
        this.flats = data;
        this.selectedFlat = this.flats[0];
      })
  },
  methods: {
    filterFlats: function(e){
      this.query = e.currentTarget.value;
      this.flats = this.allFlats.filter((flat) => new RegExp(this.query, 'i').exec(flat.name))
    },
    changedSelectedFlat: function(flat){
      console.log(flat)
      this.selectedFlat = flat;
    }
  },
}
</script>

<style scoped>
.container {
  display: flex;
}

.main {
  display: flex;
  flex-basis: 60%;
  flex-direction: column;
}

.search {
  padding: 10px;
}

.search input {
  width: 100%;
  height: 30px;
  font-size: 18px;
}

.flats {
  display: flex;
  flex-wrap: wrap;
}

.panel {
  height: 100vh;
  flex-basis: 40%;
  top: 0;
  position: sticky;
}
</style>
