<template>
  <div class="filters-container">
    <img
      class="filter-img"
      v-if="isMobile"
      @click="setFilters"
      src="times-circle-solid.svg"
    />
    <h4 @click="swapMenuState('gender')">
      <span
        >Sexe
        <span v-if="activeFilters.gender.length != 0"
          >({{ activeFilters.gender.length }})</span
        ></span
      ><img
        id="gender-arrow"
        v-if="!isMobile"
        class="drop-menu"
        src="chevron-down-solid.svg"
      />
    </h4>
    <span id="gender-menu" class="filter-menu">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Hommes"
          v-model="activeFilters.gender"
        />Hommes</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Femmes"
          v-model="activeFilters.gender"
        />Femmes</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Mixte"
          v-model="activeFilters.gender"
        />Mixte</label
      >
    </span>
    <hr />

    <h4 @click="swapMenuState('price')">
      <span
        >Rechercher par prix<span v-if="activeFilters.price.length != 0"
          >({{ activeFilters.price.length }})</span
        ></span
      >
      <img
        id="price-arrow"
        v-if="!isMobile"
        class="drop-menu"
        src="chevron-down-solid.svg"
      />
    </h4>
    <span id="price-menu" class="filter-menu">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Moins €50"
          v-model="activeFilters.price"
        />Moins €50</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="€50 - €100"
          v-model="activeFilters.price"
        />€50 - €100</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="€100 - €150"
          v-model="activeFilters.price"
        />€100 - €150</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Plus de €150"
          v-model="activeFilters.price"
        />Plus de €150</label
      >
    </span>
    <hr />

    <h4 @click="swapMenuState('color')">
      <span
        >Couleur
        <span v-if="activeFilters.color.length != 0"
          >({{ activeFilters.color.length }})</span
        ></span
      ><img
        id="color-arrow"
        v-if="!isMobile"
        class="drop-menu"
        src="chevron-down-solid.svg"
      />
    </h4>
    <span id="color-menu" class="filter-menu-color">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Noir"
          v-model="activeFilters.color"
        /><span id="noir" class="circle" style="background: black"></span
        >Noir</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Rouge"
          v-model="activeFilters.color"
        /><span class="circle" style="background: red"></span>Rouge</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Blanc"
          v-model="activeFilters.color"
        /><span class="circle" style="background: white"></span>Blanc</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Jaune"
          v-model="activeFilters.color"
        /><span class="circle" style="background: yellow"></span>Jaune</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Vert"
          v-model="activeFilters.color"
        /><span class="circle" style="background: green"></span>Vert</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Bleu"
          v-model="activeFilters.color"
        />
        <span class="circle" style="background: blue"></span>Bleu</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Rose"
          v-model="activeFilters.color"
        /><span class="circle" style="background: pink"></span>Rose</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Gris"
          v-model="activeFilters.color"
        /><span class="circle" style="background: grey"></span>Gris</label
      >
    </span>
    <hr />

    <h4 @click="swapMenuState('sport')">
      <span
        >Sports
        <span v-if="activeFilters.sport.length != 0"
          >({{ activeFilters.sport.length }})</span
        ></span
      ><img
        id="sport-arrow"
        v-if="!isMobile"
        class="drop-menu"
        src="chevron-down-solid.svg"
      />
    </h4>
    <span id="sport-menu" class="filter-menu">
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Football"
          v-model="activeFilters.sport"
        />Football</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Basket"
          v-model="activeFilters.sport"
        />Basket</label
      >
      <label
        ><input
          type="checkbox"
          name="checkbox"
          value="Running"
          v-model="activeFilters.sport"
        />Running</label
      >
    </span>

    <span v-if="isMobile" class="fixed-bottom">
      <span class="button-container"
        ><button @click="clearFilters()">
          Effacer
          <span
            v-if="
              activeFilters.gender.length +
                activeFilters.price.length +
                activeFilters.color.length +
                activeFilters.sport.length !=
              0
            "
            >({{
              activeFilters.gender.length +
              activeFilters.price.length +
              activeFilters.color.length +
              activeFilters.sport.length
            }})</span
          ></button
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
  created() {
    window.addEventListener("resize", this.getIsMobile);
    window.addEventListener("load", this.getIsMobile);
    this.$watch(
      "activeFilters",
      function () {
        if (!this.isMobile) {
          this.$emit("filtersSet", this.activeFilters);
        }
      },
      { deep: true }
    );
  },
  methods: {
    swapMenuState(id) {
      if (document.getElementById(id + "-menu").classList.contains("hidden")) {
        document.getElementById(id + "-arrow").src = "chevron-down-solid.svg";
        document.getElementById(id + "-menu").classList.remove("hidden");
      } else {
        document.getElementById(id + "-arrow").src = "chevron-up-solid.svg";
        document.getElementById(id + "-menu").classList.add("hidden");
      }
    },
    clearFilters() {
      this.activeFilters = { gender: [], price: [], color: [], sport: [] };
    },
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
.filter-img {
  cursor: pointer;
  width: 30px;
  position: absolute;
  right: 20px;
  top: 20px;
}
hr {
  margin: 0;
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
  overflow: hidden;
  height: 100%;
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
  height: 100%;
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
  .filter-menu {
    overflow: visible;
  }
}
button {
  width: 40%;
  height: 55px;
  border-radius: 40px;
}
h4 {
  display: flex;
  justify-content: space-between;
  cursor: pointer;
  align-items: center;
}
.drop-menu {
  height: 24px;
}
.hidden {
  display: none;
}
.checked {
  background-image: url("../../public/check-solid.svg");
}
</style>
