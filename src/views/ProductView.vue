<script setup>
  import {useRoute} from "vue-router";
  import axios from "axios";
  import {onMounted, ref} from "vue";

  const route = useRoute()
  const isLoaded = ref(false)
  const product = ref({})
  const fetchProduct = async () => {
      isLoaded.value = false
      const product_req = await axios.get(`http://localhost:8000/api/products/${route.params.id}`)
      product.value = product_req.data
      isLoaded.value = true
  }
  onMounted(async () => {
      await fetchProduct()
  })
</script>

<template>
    <div class="container-sm sticky-sm-top display-flex align item-center" style="width: 17%"><img :src="product.image" class="card-img-top" :alt="product.title"></div>
            <div class="card-body">
                <h5 class="card-title">{{ product.title }}</h5>
                
                <p class="card-text">{{ product.price }}</p>
                <br><br><br><br><button class="card-button"> <br>Buy now </button>
            </div>
  <div>
      
      <div v-if="isLoaded">
          <p>{{ product.title }}</p>
      </div>
      <div v-else>
          ...loading
      </div>
  </div>
</template>
<style  scoped>
.card-body{
    display: flex;
    justify-content: center;
    align-items: center;
    border-block:square;
    border-radius: 40px;
    border-color: rgb(0, 0, 0);
    border-bottom-style :solid;
    border: size 500px;;
    text-align: center;
    border-radius:30px;
}

</style>
