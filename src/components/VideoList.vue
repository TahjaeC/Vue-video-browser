<template>
  <ul class="list-group col-md-4">
    <VideoListItem
     v-for="video in videos"
     v-bind:video="video"
     v-bind:key="video.etag"
     @videoSelect="onVideoSelect">
     <!-- Key is used to update the list in a performant fashion -->
    </VideoListItem>
  </ul>
</template>

<script>
import VideoListItem from './VideoListItem';

export default {
  name:'VideoList',
  components:{
    VideoListItem
  },
  props:['videos'],
  methods:{
    onVideoSelect(video){
      this.$emit('videoSelect', video);
    }
  }
};
</script>

<style lang="css" scoped>
</style>
