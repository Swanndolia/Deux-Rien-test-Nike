<template>
  <div class="filters-container">
    <img v-if="isMobile" @click="setFilters" src="times-circle-solid.svg" />
    <h4>Sexe</h4>
    <span class="filter-menu">
      <label><input type="checkbox" value="hommes" />Hommes</label>
      <label><input type="checkbox" value="femmes" />Femmes</label>
      <label><input type="checkbox" value="mixte" />Mixte</label>
    </span>
    <hr />

    <h4>Rechercher par prix</h4>
    <span class="filter-menu">
      <label><input type="checkbox" value="50" />Moins €50</label>
      <label><input type="checkbox" value="50, 100" />€50 - €100</label>
      <label><input type="checkbox" value="100, 150" />€100 - €150</label>
      <label><input type="checkbox" value="150" />Plus de €150</label>
    </span>
    <hr />

    <h4>Couleur</h4>
    <span class="filter-menu-color">
      <label
        ><input type="checkbox" value="black" /><span
          class="circle"
          style="background: black"
        ></span>
        Noir</label
      >
      <label
        ><input type="checkbox" value="red" /><span
          class="circle"
          style="background: red"
        ></span
        >Rouge</label
      >
      <label
        ><input type="checkbox" value="white" /><span
          class="circle"
          style="background: white"
        ></span
        >Blanc</label
      >
      <label
        ><input type="checkbox" value="yellow" /><span
          class="circle"
          style="background: yellow"
        ></span
        >Jaune</label
      >
      <label
        ><input type="checkbox" value="green" /><span
          class="circle"
          style="background: green"
        ></span
        >Vert</label
      >
      <label
        ><input type="checkbox" value="blue" /><span
          class="circle"
          style="background: blue"
        ></span
        >Bleu</label
      >
      <label
        ><input type="checkbox" value="red" /><span
          class="circle"
          style="background: rose"
        ></span
        >Rose</label
      >
      <label
        ><input type="checkbox" value="grey" /><span
          class="circle"
          style="background: grey"
        ></span
        >Gris</label
      >
    </span>
    <hr />

    <h4>Sports</h4>
    <span class="filter-menu">
      <label><input type="checkbox" value="football"/>Football</label>
      <label><input type="checkbox" value="basket"/>Basket</label>
      <label><input type="checkbox" value="running"/>Running</label>
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
