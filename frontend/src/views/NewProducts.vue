<template>
  <div>
    <header>
      <h1>Nouveautés</h1>
      <img src="" />
    </header>
    <div>
      <main><ProductsList /></main>
      <aside><ProductsFilter /></aside>
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
    return {};
  },
};
</script>

<style lang="scss" scoped>
header {
  display: flex;
  flex-direction: space-between;
  padding: 0 20px;
}
</style>
