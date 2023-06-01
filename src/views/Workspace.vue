<script setup>
import { reactive } from "vue";
import Node from "../components/Node.vue";
import html2canvas from "html2canvas";

const nodes = reactive(JSON.parse(localStorage.getItem("nodes")));

function onmove(node) {
    const id = node.id
    nodes.find(n => n.id === id).position = node.position;
    localStorage.setItem("nodes", JSON.stringify(nodes))
};

function downloadJPG() {
    html2canvas(document.querySelector("#workspace")).then(canvas => {
        const dataURL = canvas.toDataURL('image/jpeg');

        const link = document.createElement('a');
        link.href = dataURL;
        link.download = 'image.jpg';

        link.click();
    });
};

</script>
<template>
    <div id="actions">
        <button class="action-btn" @click="downloadJPG">Export JPG</button>
    </div>
    <div id="workspace">
        <Node v-for="node in nodes" :key="node.key" :node="node" @move="() => onmove(node)" />
    </div>
</template>
<style>
#workspace {
    position: relative;
    width: 100%;
    height: 100vh;
    background-color: #222;
    background-image: radial-gradient(#fff, transparent 1px);
    background-size: 20px 20px;
}

#actions {
    position: absolute;
    z-index: 100;
    left: 50%;
    translate: -50%;
}

.action-btn {
    font-size: .8em;
    margin: .2em;
    padding: .2em .4em;
}

@media(prefers-color-scheme: light) {
    #workspace {
        background-color: #fff;
        background-image: radial-gradient(#888, transparent 1px);
    }
}
</style>