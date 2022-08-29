<template>
  <div>
    <div class="header">
      <h3>List of photos</h3>
    </div>
    <b-container fluid class="mt-5">
      <PhotoGridSkeleton v-if="!isMounted" />
      <b-container v-else class="mt-5">
        <b-row cols="4">
          <b-col v-for="(item,index) in currentImageCards" :key="index" col no-gutters>
            <PhotoGrid :item="item" :key="index" :showCompare="showCompare(item)" @compare-remove="compareRemove"  />
          </b-col>
        </b-row>
        <bPagination align="center" :total-rows="pageCount" v-model="currentPageIndex" :per-page="imagesPerPage"
                     @change="pageClick(currentPageIndex)" class="mt-5"></bPagination>
      </b-container>
    <ComparisonTable :fields="fields" :items="compareditems" />
    </b-container>
  </div>
</template>

<script>
import ComparisonTable from "@/components/ComparisonTable";
import PhotoGrid from "@/components/PhotoGrid";
import PhotoGridSkeleton from "@/components/PhotoGridSkeleton";
export default {
  name: 'PhotoList',
  components: {PhotoGrid, ComparisonTable, PhotoGridSkeleton},
  data() {
    return {
      fields:[{ key: 'thumbnailUrl', label:'' },
      { key: 'id', label: 'ID' },
      { key: 'url', label: 'URL' },
      { key: 'title', label: 'Title' },],
      compareditems: [],
      images: [],
      paginateImages: [],
      imagesPerPage: 4,
      currentPageIndex: 1,
      pageCount: 0,
      isMounted: false,
    }
  },
  computed: {
    currentImageCards(){
      this.createPages();
      return this.paginateImages[this.currentPageIndex];
    }
  },
  mounted() {
    this.axios.get('https://jsonplaceholder.typicode.com/photos').then((response) => {
      this.images = response.data;
      this.isMounted = true;
    })
  },
  methods:{
    compareRemove(item) {
      const isFound = this.compareditems.findIndex(element => {
        return element.id === item.id
      });
      if(isFound === -1) {
        this.compareditems.push(item)
      }
      else{
        this.compareditems.splice(isFound,1);
      }
    },
    showCompare(item) {
      const isFound = this.compareditems.findIndex(element => {
        return element.id === item.id
      });
      if(isFound === -1) {
        return true
      }
      return false
    },
    createPages() {
      let imageLength = this.images.length;
      let fullPagesCount = Math.floor(imageLength/this.imagesPerPage);

      if(imageLength>this.imagesPerPage) {
        this.pageCount = 0;
        for (let i = 0; i < fullPagesCount * this.imagesPerPage; i += this.imagesPerPage) {
          this.paginateImages[this.pageCount] = this.images.slice(i,i + this.imagesPerPage);
          this.pageCount++;
        }

        this.paginateImages[this.pageCount] = this.images.slice(imageLength-this.imagesPerPage,imageLength);
        this.pageCount = this.pageCount+1;
      } else {
        this.paginateImages[0] = this.images;
      }
    },
    pageClick(i){
      this.currentPageIndex=i;
    }
  }
}
</script>
<style scoped>
.card-columns .card {
  max-width: calc(25% - 30px);
}
.header{
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px 5px;
  background-color: #111046;
  color: #fff;
  text-transform: uppercase;
}
</style>
