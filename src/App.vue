<template>
  <div class="wrapper">
    <select v-model="selectedCategory">
      <option value="">All Categories</option>
      <option v-for="category in categories" :key="category">
        {{ category }}
      </option>
    </select>

    <input
      type="text"
      v-model="searchQuery"
      placeholder="Search Product"
    />
    <!--used to create a two-way binding between a form input element-->
    <div class="card-body">
      <div v-for="product in filteredProducts" :key="product.id">
        <div class="card-header">
          <h3>{{ product.name }}</h3>
        </div>
        <img :src="product.image" :alt="product.name" loading="lazy" />
        <div class="card-footer">
          <p :class="product.price">R{{ product.price }}.00</p>
        </div>
      </div>
    </div>

    <p v-if="filteredProducts.length === 0">No products found.</p>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    //Reactive state
    return {
      products: [
        {
          id: 1,
          name: "VW Golf 7 GTI Front Lip",
          image:
            "https://i.postimg.cc/fyz3wyPw/eng-pm-FRONT-SPLITTER-VW-GOLF-VII-GTI-FACELIFT-V-1-959-1.jpg",
          price: "1500",
          category: "Golf",
        },
        {
          id: 2,
          name: "BMW F30 Rear Diffuser",
          image:
            "https://i.postimg.cc/JhnwK3v3/image-c814c26f-32e2-40d5-8b2a-a4ea4652d787.webp",
          price: "2900",
          category: "Bmw",
        },
        {
          id: 3,
          name: "VW Golf 7 GTI Rear Spoiler",
          image:
            "https://i.postimg.cc/rmJmYcw7/Spoiler-Extention-0002-Layer-3.jpg",
          price: "1900",
          category: "Golf",
        },
        {
          id: 4,
          name: "BMW M3 F80 Boot Spoiler",
          image:
            "https://i.postimg.cc/15Fgs0gm/image-0c86151c-0c56-46b7-ae50-b71afc9c9ea8.webp",
          price: "2500",
          category: "Bmw",
        },
        {
          id: 5,
          name: "VW Golf 7 GTI Rear Diffuser",
          image:
            "https://i.postimg.cc/4xWbvpzT/image-27efa4c9-7222-43ac-8150-314305ad3558-1880x.webp",
          price: "1700",
          category: "Golf",
        },
        {
          id: 6,
          name: "BMW 135i Rear Diffuser",
          image:
            "https://i.postimg.cc/k5d9ct9f/image-e8f5128f-4c38-4841-89cd-434773cbba13.webp",
          price: "1900",
          category: "Bmw",
        },
      ],
      selectedCategory: "",
      searchQuery: "",
    };
  },
  components: {},
  computed: {
    categories() {
      return [...new Set(this.products.map((product) => product.category))];
    },
    filteredProducts() {
      let filtered = this.products;

      if (this.selectedCategory) {
        filtered = filtered.filter(
          (product) => product.category === this.selectedCategory
        );
      }

      if (this.searchQuery) {
        filtered = filtered.filter((product) =>
          product.name.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      }

      return filtered;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
