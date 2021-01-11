<template>
    <button type="button" class="btn btn-danger btn-lg" @click="$emit('removeAll')">Clear all tasks</button>
</template>

<script>
// import Vue from 'vue';

export default {
  name: 'ClearAllBtn',
  props: ['title', 'key'],
  emits: ['removeAll']
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    button {
        float: right;
        clear: both;
    }

    li {
        text-align: center;
        padding-left: 40px;
    }
</style>