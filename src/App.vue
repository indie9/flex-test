<template>
  <div class="flex">
    <template v-for="(image, index) in images" :key="index">
      <div class="item">
        <img :src="image.webformatURL" alt="Image" class="img" @load="fadeIn" :width="image.webformatWidth / 2"
          :height="image.webformatHeight / 2">
      </div>
      <div v-if="(index % 2) && index" class="wrapmedia"></div>
      <div class="wrapmedia800"></div>
    </template>
  </div>
</template>


<script >

import axios from 'axios'
export default {
  data() {
    return {
      images: []
    }
  },
  mounted() {
    axios.get('https://pixabay.com/api/?key=42222643-e80ebcf1b7d2eedcc5912e497&per_page=20')
      .then(({ data }) => {
        this.images = [...(data?.hits || [])]
      })
  },
  methods: {
    fadeIn(event) {
      event.target.style.opacity = 1;
    },
  }
}

</script>


<style scoped>
.flex {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  margin: 5px;
  background: #FFFFFF;
}

.item {
  width: calc(50% - 10px);
  margin: 5px;
  height: fit-content;
}

.img {
  border-radius: 5px;
  object-fit: contain;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 1s;
  box-shadow: 0px 5px 10px 2px rgba(39, 80, 34, 0.2);
}

.wrapmedia{
  width: 100%;
  display: block;
}

.wrapmedia800{
  display: none;
}

@media screen and (max-width: 800px) {
  .item {
    width: 100%;

  }

  .wrapmedia {
    display: none;
  }

  .wrapmedia800 {
    display: block;
    width: 100%;
  }
}
</style>
