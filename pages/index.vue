<template>
  <div class="home">
    <div class="first-view">
      <div class="firstview_ttl">
        <p class="firstview_txt">New Arrivals</p>
        <p class="firstview_txt fbg">for BOYS & GIRLS</p>
      </div>
      
    </div>
    <div class="products">
      <h2 class="products_ttl">Product</h2>
      <div class="flex ">
        <div c class="product-items" v-for="product in products" :key="product.id">
          <div class="test" @click="$router.push({path: '/detail/' + product.id,params: {id: product.id}})">
            <img :src="product.img_url" alt="sandal_img" class="product_img" />
            <p>{{product.product_name}}</p>
            <p>¥<span>{{product.price}}</span>(税込)</p>
          </div>
        </div>
      </div>
      
    </div>
    <div class="nav">
      <div
        class="prev"
        @click="clickPrevNewsPage()"
      >
      <p>[prev]</p>
      </div>
      <ul>
        <li>
          ページ番号
        </li>
      </ul>
    </div>
    <div 
      class="next"
      @click="clickNextPage()"
    >
    <p>[next]</p>
    </div>
  </div>
</template>

<script>
export default {
  middleware: "auth",
  data() {
    return {
      products: null
    };
  },
  methods: {
    async showProduct() {
      await this.$axios.get("http://127.0.0.1:8000/api/product").then(res => {
        console.log(res.data.data);
        this.products = res.data.data;
      });
    }
  },
  async created() {
    await this.showProduct();
  }
};
</script>

<style scoped>
p {
  margin: 0;
}
.first-view {
  position: relative;
  background-image: url('../assets/sandal.jpg');
  background-position: center;
  background-size: cover;
  height: 1200px;
  margin-top: 10px;
  
}
.firstview_ttl {
  position: absolute;
  top: 30%;
  right: 10%;
  font-size: 72px;
  margin: 0;
  
}

.firstview_txt {
  margin: 0;
}

.fbg {
  font-size: 35px;
}

.flex {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
}

.products_ttl {
  text-align: center;
  font-size: 45px;
  margin: 10px 0;
}

.product-items {
  width: 25%;
}


.product__item {
  display: flex;
}

.product_img {
  width: 90%;
  height: 250px;
  object-fit: cover;
  object-position: 50% 50%;
}
</style>
