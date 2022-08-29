<template>
  <b-card
      align="'center"
      tag="article"
      style="max-width: 20rem;"
      class="mb-2 article-list"
  >
    <template #header>
      <img :src="item.thumbnailUrl" class="banner-image" @error="onImageError">
    </template>
    <b-col><h6>{{ item.title | capitalize }}</h6></b-col>
    <b-col><h6>ID {{item.id}}</h6></b-col>
    <b-col><div class="urldiv"><a :href="item.url" target="_blank">{{item.url}}</a></div></b-col>
    <template #footer >
      <b-col style="width: 100%;">
        <b-button style="width: 100%;" @click="$emit('compare-remove',item)" :variant="showCompare ? 'info' : 'danger'">
          {{ showCompare ? 'Compare' : 'Remove' }}</b-button>
      </b-col>
    </template>
  </b-card>
</template>

<script>
import Constant from "./../Constant";
let failedImage = require('../assets/dummy.png');
export default {
  name: 'PhotoGrid',
  props: {
    item: Object,
    showCompare: Boolean,
  },
  data(){
    return {
      dummyImgURL : Constant.DUMMY_IMG_URL,
    }
  },
  methods: {
    onImageError(e){
      e.target.src = failedImage;
    }
  },
  filters:{
    capitalize(text){
      return text.charAt(0).toUpperCase() + text.slice(1)
    }
  }
}
</script>
<style scoped="true">
.banner-image {height: 150px;width: 100%}
a{text-decoration: none;}
.article-list {border: 0; box-shadow: 0 10px 22px 0 rgb(0 0 0 / 15%);}
.article-list h6{min-height:40px; display: -webkit-box; -webkit-line-clamp:2; -webkit-box-orient: vertical;  overflow: hidden;}
.urldiv{min-height:48px;}

</style>
