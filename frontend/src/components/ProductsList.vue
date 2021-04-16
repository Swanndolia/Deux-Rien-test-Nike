<template>
  <div class="products-container">
    <figure v-for="product in getMatchingProducts" :key="product.key">
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
  props: { activeFilters: Object },
  computed: {
    getMatchingProducts() {
      const that = this;
      if (
        Object.keys(this.activeFilters).every(function (key) {
          return that.activeFilters[key].length === 0;
        })
      ) {
        this.$emit("totalProductsMatching", this.productsList.length);
        return this.productsList;
      } else {
        let filteredProductsList = [];
        Object.keys(this.productsList).forEach(function (key) {
          const priceArray = that.activeFilters.price
            .join("-")
            .replace("Moins", "0 - ")
            .replace("Plus", "9999 - ")
            .replaceAll(/[^0-9-]+/g, "")
            .split("-")
            .slice()
            .sort(function (a, b) {
              return a - b;
            });
          if (
            //filter by gender
            (that.activeFilters.gender == "" ||
              that.activeFilters.gender
                .join("")
                .includes(that.productsList[key].sexe)) &&
            //filter by price
            (that.activeFilters.price == "" ||
              (parseInt(priceArray[0]) <=
                parseInt(
                  that.productsList[key].prix
                    .replace("€", "")
                    .split(",")
                    .shift()
                ) &&
                parseInt(priceArray[priceArray.length - 1]) >=
                  parseInt(
                    that.productsList[key].prix
                      .replace("€", "")
                      .split(",")
                      .shift()
                  ))) &&
            //filter by color
            (that.activeFilters.color == "" ||
              that.activeFilters.color
                .join(",")
                .toLowerCase()
                .split(",")
                .some((r) =>
                  that.productsList[key].couleur
                    .toLowerCase()
                    .split(", ")
                    .includes(r)
                )) &&
            //filter by sport
            (that.activeFilters.sport == "" ||
              that.activeFilters.sport
                .join("")
                .includes(that.productsList[key].sport))
          ) {
            that.$emit("totalProductsMatching", filteredProductsList.length);
            filteredProductsList.push(that.productsList[key]);
          }
        });
        return filteredProductsList;
      }
    },
  },
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
