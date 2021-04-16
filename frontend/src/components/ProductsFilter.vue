<template>
  <div class="filters-container">
    <h4>Sexe</h4>
    <span class="filter-menu">
      <label><input type="checkbox" />Hommes</label>
      <label><input type="checkbox" />Femmes</label>
      <label><input type="checkbox" />Mixte</label>
    </span>
    <hr />

    <h4>Rechercher par prix</h4>
    <span class="filter-menu">
      <label><input type="checkbox" />Moins €50</label>
      <label><input type="checkbox" />€50 - €100</label>
      <label><input type="checkbox" />€100 - €150</label>
      <label><input type="checkbox" />Plus de €150</label>
    </span>
    <hr />

    <h4>Couleur</h4>
    <span class="filter-menu-color">
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: black"
        ></span>
        Noir</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: red"
        ></span
        >Rouge</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: white"
        ></span
        >Blanc</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: yellow"
        ></span
        >Jaune</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: green"
        ></span
        >Vert</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: blue"
        ></span
        >Bleu</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: rose"
        ></span
        >Rose</label
      >
      <label
        ><input type="checkbox" /><span
          class="circle"
          style="background: grey"
        ></span
        >Gris</label
      >
    </span>
    <hr />

    <h4>Sports</h4>
    <span class="filter-menu">
      <label><input type="checkbox" />Football</label>
      <label><input type="checkbox" />Basket</label>
      <label><input type="checkbox" />Running</label>
    </span>

    <span class="fixed-bottom">
      <span class="button-container"
        ><button @click="clearFilters()">Effacer</button
        ><button @click="setFilters()">Appliquer</button></span
      ></span
    >
  </div>
</template>

<script>
export default {
  name: "ProductsFilter",
  components: {},
  data() {
    return {};
  },
  methods: {
    setFilters() {
      this.$emit("filtersSet", true);
    },
  },
};
</script>

<style lang="scss" scoped>
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
  max-height: calc(100vh - 60px);
  overflow-y: scroll;
}
.filter-menu {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  line-height: 220%;
}
.fixed-bottom {
  bottom: calc(0% - 15px);
  height: 60px;
  left: 25%;
}
.button-container {
  position: relative;
  display: flex;
  justify-content: space-around;
  background: white;
  gap: 30%;
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
label, input, circle{
  cursor: pointer;
  &:hover{
    color: lighten(black, 30%);
  }
}
@media screen and (max-width: 1024px) {
  .fixed-bottom {
    position: fixed;
  }
  hr{
      margin: 20px 0;
  }
}
</style>
