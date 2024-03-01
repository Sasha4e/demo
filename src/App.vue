
<template>

    <div class="wrapper">
        <div class="header">
            <h1>Header</h1>
        </div>
        <div class="content">
            <div class="aside">
               <p>Sidebar</p>
            </div>
            <div class="main">
                <div class="dndflow" @drop="onDrop">
                    <Sidebar />
                    <VueFlow :nodes="nodes" @dragover="onDragOver" @dragleave="onDragLeave" v-model="nodes">
                        <DropzoneBackground
                            :style="{
          backgroundColor: isDragOver ? '#e7f3ff' : 'transparent',
          transition: 'background-color 0.2s ease',
        }"
                        />
                    </VueFlow>


                </div>
            </div>

        </div>

    </div>





</template>

<script setup>
import { ref } from 'vue'
import { VueFlow, useVueFlow, Position } from '@vue-flow/core'
import DropzoneBackground from '@/components/DropzoneBackground.vue'
import Sidebar from '@/components/Sidebar.vue'
import useDragAndDrop from '@/components/useDnD.js'
const { onConnect, addEdges, onNodeDragStop } = useVueFlow();


const { onDragOver, onDrop, onDragLeave, isDragOver } = useDragAndDrop()

const nodes = ref([])
const defaultNodeStyle = {
    border: '1px solid #10b981',
    borderRadius: '99px',
    height: '100px',
    width: '100px',
    textAlign: 'center',
    display: 'flex',
    alignItems: 'center',
    justifyContent: 'center'
}
const elements = ref([

    { id: '1', type: 'input', label: 'Node 1', position: { x: 250, y: 5 } },
    { id: '2', label: 'Node 2', position: { x: 100, y: 100 }, },
    { id: '3', type: 'output', label: 'Node 3', position: { x: 400, y: 200 } },

    {
        id: '4',
        type: 'special',
        label: 'Node 4',
        position: { x: 400, y: 300 },
        style: defaultNodeStyle,
    },
    {
        id: '5',
        label: 'toolbar right',
        data: { toolbarPosition: Position.Right },
        position: { x: 350, y: 100 },

    },


    { id: 'e1-3', source: '1', target: '3' },
    { id: 'e1-2', source: '1', target: '2' },
    {
        id: 'e1-4',
        type: 'special',
        source: '1',
        target: '4',
        data:  'world',

    },
])
onConnect(addEdges)
onNodeDragStop(( node) => {
    console.log('Node Drag Stop', node)
    console.log('Nodes ', nodes.value)
})
</script>
<style>
@import '@vue-flow/core/dist/style.css';
@import '@vue-flow/core/dist/theme-default.css';
.header {
    border: 1px solid grey;
}
.content {
    height: 100vh;
    display: flex;
    border: 1px solid grey;
}
.aside {
    flex: 1;
    border: 1px solid grey;
}
.main {
    width: 100%;
    display: flex;

    flex: 6
}

</style>