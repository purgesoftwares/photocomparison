<template>
  <b-container fluid>
    <b-row cols="4">
      <b-col v-for="(item,index) in [1,2,3,4]" :key="index" col no-gutters>
        <b-card no-body img-top>
          <b-skeleton-img card-img="top" aspect="3:1"></b-skeleton-img>
          <b-card-body>
            <b-skeleton />
            <b-skeleton />
            <b-skeleton />
          </b-card-body>
          <template #footer>
            <b-skeleton />
          </template>
        </b-card>
      </b-col>
    </b-row>
  </b-container>
</template>


BP816333517   wbtc pending me hai


<script>

export default {
  name: 'PhotoGridSkeleton',
}
</script>
