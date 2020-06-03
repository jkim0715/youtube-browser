<template>
  <div class="search-bar">
      <input class="input" @keypress.enter="onInput">
  </div>
</template>

<script>
export default {
    name:"SearchBar",
    methods:{
        onInput(event) {
            // console.log(event.target.value)
            this.$emit('input-change', event.target.value)
        }
    }
}
</script>

<style scoped>
	div .search-bar{
        text-align: center;
        margin: 20px;
    }
    div .input {
        width:75%
    }
</style>