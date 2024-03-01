<script setup>
import useDragAndDrop from './useDnD.js'

const { onDragStart } = useDragAndDrop()
</script>

<template>
    <aside class="custom-aside">


        <div class="nodes">
            <div class="vue-flow__node-input" :draggable="true" @dragstart="onDragStart($event, 'input')">Input Node</div>

            <div class="vue-flow__node-default" :draggable="true" @dragstart="onDragStart($event, 'default')">Default Node</div>

            <div class="vue-flow__node-output" :draggable="true" @dragstart="onDragStart($event, 'output')">Output Node</div>
        </div>
    </aside>
</template>

<style langs="scss" scoped>
.custom-aside {
    display: flex;
    justify-content: center;
}
</style>