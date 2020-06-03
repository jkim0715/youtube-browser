<template>
    <li @click="onVideoSelect" class="video-list-item list-group-item">
        <img :src="thumbnailUrl" alt="" class="mr-3">
        <div class="media-body">
            <h4 v-html="video.snippet.title"></h4>
        </div>
    </li>
</template>

<script>
    export default {
        name: 'VideoListItem',
        props: {
            video: Object,
        },
        methods: {
            onVideoSelect() {
                this.$emit('video-select', this.video) // video selected
            },
        },
        computed: {
            // 함수지만 명사 네이밍 => 결국 리턴되는 값으로 사용되기 때문
            thumbnailUrl() {
                return this.video.snippet.thumbnails.default.url
            }
        },
    }
</script>

<style>
    li.video-list-item {
        display: flex;
        cursor: pointer;
    }
    li.video-list-item:hover {
        background-color: #eee;
    }
    .media-body {
        margin: auto 0;
    }
</style>