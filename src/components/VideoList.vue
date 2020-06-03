<template>
    <ul class="list-group col-lg-4">
        <!-- <li v-for="video in videos" :key="video.etag"> {{video.snippet.description}}</li> => 컴포넌트(VideoListItem)로 교체  -->
        <VideoListItem @video-select="onVideoSelect" v-for="video in videos" :video="video" :key="video.etag" />
    </ul>
</template>

<script>
    import VideoListItem from './VideoListItem.vue'
    export default {
        name: 'VideoList',
        components: {
            VideoListItem
        },
        props: {
            videos: Array,
        },
        methods: {
            onVideoSelect(selectedvideo) { // 다른 컴포넌트에서 이미 사용했던 함수 내용을 활용해도 무방하다 => 분리되어있기 때문
                this.$emit('video-select', selectedvideo) // emit하는 함수이름도 겹쳐도 상관 없는게 부모한테만 쏠 수 있기 때문에.
            }
        },

    }
</script>

<style>

</style>