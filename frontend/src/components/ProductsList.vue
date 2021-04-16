<template>
  <div class="products-container">
    <figure v-for="product in productsList" :key="product.key">
      <img :src="'photos_produits/' + product.photo" />
      <figcaption>
        <strong>{{ product.article }}</strong
        ><br />{{ getProductGender(product.sexe) }}<br />{{
          getProductcolor(product.couleur)
        }}<br />{{ getProductPrice(product.prix) }}
      </figcaption>
    </figure>
  </div>
</template>

<script>
import jsonProducts from "../assets/produits.json";
export default {
  name: "ProductsList",
  components: {},
  data() {
    return { productsList: jsonProducts };
  },
  computed: {},
  mounted() {
    console.log(this.productsList);
  },
  methods: {
    getProductGender(gender) {
      return gender;
    },
    getProductcolor(color) {
      return color.split(",").length + (color.split(",").length > 1 ? " couleurs" : " couleur");
    },
    getProductPrice(price) {
      return price;
    },
  },
};
</script>

<style lang="scss" scoped>
.products-container {
  overflow: hidden;
  width: 100%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
figure {
  flex: 50%;
  margin: 20px 0;
}
figcaption {
  text-align: left;
  padding-left: 5px;
}
img {
  max-width: 100%;
}
</style>
