<template>
    <li @click="$emit('complete')" draggable>
        {{ title }}
        <button type="button" class="btn-close btn-close-white" aria-label="Close" @click="$emit('remove')"></button>
    </li>
</template>

<script>
// import Vue from 'vue';

export default {
  name: 'ToDoListTasks',
  props: ['title', 'key'],
  emits: ['remove','complete']
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
