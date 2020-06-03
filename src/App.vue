<template>
  <div class="container mt-5">
    <!-- 검색 창 -->
    <SearchBar @input-change="onInputChange" />
    <div class="row">
      <VideoDetail :selectedVideo="selectedVideo" />
      <!-- data로 저장 안하고 바로 보내기 가능?? -->
      <!-- 데이터로 저장 한번 해야 App에 들리는 거라고 할 수 있다. -->
      <VideoList  
      @video-select="onVideoSelect" 
      :videos="videos"
      />
    </div>


  </div>
</template>

<script>
import axios from 'axios'

import SearchBar from './components/SearchBar.vue'
import VideoList from './components/VideoList.vue'
import VideoDetail from './components/VideoDetail.vue'

const API_KEY = process.env.VUE_APP_YOUTUBE_API_KEY
const API_URL = "https://www.googleapis.com/youtube/v3/search"

export default {
  name: 'App',
  components: {
      SearchBar,VideoList,VideoDetail
  },
  data() {
    return{
      inputValue: '',
      videos: [],
      selectedVideo: null,
    }
  },
  methods:{
    onInputChange(data) {
      this.inputValue = data
      axios.get(API_URL, {params:{
        key: API_KEY,
        part:'snippet',
        type:'video',
        q: this.inputValue
      }
      }) .then(res => {
        res.data.items.forEach(item =>{
          let parser = new DOMParser()
          let doc = parser.parseFromString(item.snippet.title, 'text/html')
          item.snippet.title = doc.body.innerText
        })
          this.videos = res.data.items
        }) 
        .catch(err => console.log(err))
    },
    onVideoSelect(video) {
      this.selectedVideo= video
    },
  },
}
</script>

<style>


</style>
