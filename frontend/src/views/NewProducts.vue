<template>
  <div id="root">
    <header>
      <h1>Nouveautés {{ getActiveFilters }} ({{ productCount }})</h1>
      <img src="sliders-h-solid.svg" @click="displayFilters()" />
    </header>
    <div class="main-container">
      <aside>
        <ProductsFilter
          @isDesktop="hideFilters()"
          @filtersSet="
            hideFilters();
            setFilters($event);
          "
        />
      </aside>
      <main>
        <ProductsList
          @totalProductsMatching="updateProductCount($event)"
          :activeFilters="activeFilters"
        />
      </main>
    </div>
  </div>
</template>

<script>
import ProductsFilter from "../components/ProductsFilter.vue";
import ProductsList from "../components/ProductsList.vue";
export default {
  name: "NewProducts",
  components: { ProductsFilter, ProductsList },
  data() {
    return {
      activeFilters: { gender: [], price: [], color: [], sport: [] },
      productCount: Number,
    };
  },
  computed: {
    getActiveFilters() {
      let activeFiltersList = [];
      for (const array in this.activeFilters) {
        activeFiltersList.push(this.activeFilters[array].join(" "));
      }
      return activeFiltersList.join(" ");
    },
  },
  methods: {
    updateProductCount(e) {
      this.productCount = e;
    },
    displayFilters() {
      document.getElementsByTagName("aside")[0].classList.add("displayed");
      document.getElementsByTagName("main")[0].style.display = "none";
    },
    hideFilters() {
      document.getElementsByTagName("aside")[0].classList.remove("displayed");
      document.getElementsByTagName("main")[0].style.display = "flex";
    },
    setFilters(e) {
      this.activeFilters = e;
    },
  },
};
</script>

<style lang="scss" scoped>
aside {
  flex-basis: 280px;
  transition: 0.4s;
}
main {
  flex-basis: 100%;
}
#root {
  max-width: 1920px;
  margin: 0px auto;
}
img {
  height: 20px;
  display: none;
  cursor: pointer;
}
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  font-size: 18px;
  height: 67px;
}
h1 {
  line-height: 100%;
  font-size: 18px;
  font-weight: 300;
}
.main-container {
  display: flex;
  flex-direction: row;
  gap: 50px;
}
.displayed {
  top: 0;
  background: white;
  display: flex;
  position: absolute;
  width: 100%;
  height: 100%;
}
@media screen and (max-width: 1024px) {
  aside {
    display: none;
  }
  img {
    display: initial;
  }
}
</style>
