<template>
  <div class="products-container">
    <figure v-for="product in productsList" :key="product.key">
      <img :src="'photos_produits/' + product.photo" />
      <figcaption>
        <strong>{{ product.article }}</strong
        ><br />{{ getProductGender(product.sexe) }}<br />{{
          getProductcolor(product.couleur)
        }}
        <p style="color: black">
          {{ product.prix }}
        </p>
      </figcaption>
    </figure>
  </div>
</template>

<script>
import jsonProducts from "../assets/produits.json";
import jsonWebpProducts from "../assets/produits_webp.json";
export default {
  name: "ProductsList",
  components: {},
  data() {
    return { productsList: [] };
  },
  computed: {},
  mounted() {
    const isIE = /*@cc_on!@*/ false || !!document.documentMode;
    isIE
      ? (this.productsList = jsonProducts)
      : (this.productsList = jsonWebpProducts);
  },
  methods: {
    getProductGender(gender) {
      return (
        "Chaussure" +
        (gender == "Homme"
          ? " pour Homme"
          : gender == "Femme"
          ? " pour Femme"
          : "")
      );
    },
    getProductcolor(color) {
      return (
        color.split(",").length +
        (color.split(",").length > 1 ? " couleurs" : " couleur")
      );
    },
  },
};
</script>

<style lang="scss" scoped>
.products-container {
  overflow: hidden;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
figure {
  flex: 30%;
  margin: 0 1% 15px 0;
  cursor: pointer;
}
figcaption {
  margin: 10px;
  font-size: 14px;
  line-height: 150%;
  color: grey;
}
img {
  max-width: 100%;
}
strong {
  color: black;
}
@media screen and (max-width: 1024px) {
  figure {
    flex: 49%;
  }
}
</style>
