<template>
  <div class="filters-container">
    <img v-if="isMobile" @click="setFilters" src="times-circle-solid.svg" />
    <h4>
      Sexe<span v-if="activeFilters.gender.length != 0">
        ({{ activeFilters.gender.length }})</span
      >
    </h4>
    <span class="filter-menu">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="hommes"
          v-model="activeFilters.gender"
        />Hommes</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="femmes"
          v-model="activeFilters.gender"
        />Femmes</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="mixte"
          v-model="activeFilters.gender"
        />Mixte</label
      >
    </span>
    <hr />

    <h4>
      Rechercher par prix<span v-if="activeFilters.price.length != 0">
        ({{ activeFilters.price.length }})</span
      >
    </h4>
    <span class="filter-menu">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="50"
          v-model="activeFilters.price"
        />Moins €50</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="50, 100"
          v-model="activeFilters.price"
        />€50 - €100</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="100, 150"
          v-model="activeFilters.price"
        />€100 - €150</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="150"
          v-model="activeFilters.price"
        />Plus de €150</label
      >
    </span>
    <hr />

    <h4>
      Couleur<span v-if="activeFilters.color.length != 0"
        >({{ activeFilters.color.length }})</span
      >
    </h4>
    <span class="filter-menu-color">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="black"
          v-model="activeFilters.color"
        /><span class="circle" style="background: black"></span> Noir</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="red"
          v-model="activeFilters.color"
        /><span class="circle" style="background: red"></span>Rouge</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="white"
          v-model="activeFilters.color"
        /><span class="circle" style="background: white"></span>Blanc</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="yellow"
          v-model="activeFilters.color"
        /><span class="circle" style="background: yellow"></span>Jaune</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="green"
          v-model="activeFilters.color"
        /><span class="circle" style="background: green"></span>Vert</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="blue"
          v-model="activeFilters.color"
        /><span class="circle" style="background: blue"></span>Bleu</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="red"
          v-model="activeFilters.color"
        /><span class="circle" style="background: rose"></span>Rose</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="grey"
          v-model="activeFilters.color"
        /><span class="circle" style="background: grey"></span>Gris</label
      >
    </span>
    <hr />

    <h4>
      Sports<span v-if="activeFilters.sport.length != 0"
        >({{ activeFilters.sport.length }})</span
      >
    </h4>
    <span class="filter-menu">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="football"
          v-model="activeFilters.sport"
        />Football</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="basket"
          v-model="activeFilters.sport"
        />Basket</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="running"
          v-model="activeFilters.sport"
        />Running</label
      >
    </span>

    <span v-if="isMobile" class="fixed-bottom">
      <span class="button-container"
        ><button @click="clearFilters()">Effacer</button
        ><button style="background: black; color: white" @click="setFilters()">
          Appliquer
        </button></span
      ></span
    >
  </div>
</template>

<script>
export default {
  name: "ProductsFilter",
  components: {},
  data() {
    return {
      activeFilters: { gender: [], price: [], color: [], sport: [] },
      isMobile: false,
    };
  },
  computed: {},
  mounted() {
    window.addEventListener("resize", this.getIsMobile);
    window.addEventListener("load", this.getIsMobile);
  },
  methods: {
    setFilters() {
      this.$emit("filtersSet", this.activeFilters);
    },
    getIsMobile() {
      if (window.innerWidth > 1024) {
        this.$emit("isDesktop", true);
        this.isMobile = false;
      } else {
        this.isMobile = true;
      }
    },
  },
};
</script>

<style lang="scss" scoped>
img {
  cursor: pointer;
  width: 30px;
  position: absolute;
  right: 20px;
  top: 20px;
}
hr {
  margin: 20px 0 0 0;
  border-bottom: none;
}
.filters-container {
  padding: 0 20px;
  width: 100%;
  position: relative;
  display: flex;
  flex-direction: column;
  max-height: calc(100vh - 70px);
  overflow-y: scroll;
}
.filter-menu {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  line-height: 220%;
}
.fixed-bottom {
  bottom: calc(0% - 35px);
  height: 100px;
  width: 100%;
  margin-left: -20px;
}
.button-container {
  position: relative;
  display: flex;
  justify-content: space-around;
  background: white;
}
.filter-menu-color {
  display: flex;
  flex-direction: row;
  justify-content: center;
  flex-wrap: wrap;
  & label {
    display: flex;
    flex-basis: 33%;
    flex-direction: column;
    align-items: center;
    font-size: 13px;
  }
  & input {
    display: none;
  }
}
.circle {
  height: 28px;
  width: 28px;
  border-radius: 50%;
  border: 1px solid grey;
  margin: 10px;
}
label,
input,
circle {
  cursor: pointer;
  &:hover {
    color: lighten(black, 30%);
  }
}
@media screen and (max-width: 1024px) {
  .fixed-bottom {
    position: fixed;
  }
  hr {
    margin: 20px 0;
  }
}
button {
  width: 40%;
  height: 55px;
  border-radius: 40px;
}
</style>
