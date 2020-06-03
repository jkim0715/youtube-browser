<template>
  <div v-if="selectedVideo" class="col-lg-8">
    <div class="embed-responsive embed-responsive-16by9">
      <iframe class="embed-responsive-item" :src="video_url" allowfullscreen></iframe>
    </div>
    <div class="details">
      <!-- Inner HTML이 가끔 안전하지 않을 때가 있습니다. -->
      <h4 v-text="selectedVideo.snippet.title"></h4>
      <p>
        {{selectedVideo.snippet.description}}
      </p>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'VideoDetail',
    props: {
      selectedVideo: Object,
    },
    computed: {
      video_url() {
        return `https://youtube.com/embed/${this.selectedVideo.id.videoId}`
      }
    }
  }
</script>

<style scoped>
  div.details {
    margin-top: 10px;
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
  }
</style>