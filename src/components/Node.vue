<script setup>
import { ref, onMounted } from "vue";
import Title from "./NodeTitle.vue";
import Element from "./NodeElement.vue"

const props = defineProps({ node: Object });
const emit = defineEmits(["move"]);
const nodeElement = ref();

onMounted(() => {
    nodeElement.value.style.left = props.node.position.x + "px";
    nodeElement.value.style.top = props.node.position.y + "px";
});

let nodeStartPos, pointerStartPos, delta;

function ondragstart(e) {
    nodeStartPos = {
        x: parseInt(nodeElement.value.style.left) || 0,
        y: parseInt(nodeElement.value.style.top) || 0
    };
    pointerStartPos = {
        x: e.x,
        y: e.y
    };
};

function ondrag(e) {
    if (e.x && e.y) {
        delta = { x: e.x - pointerStartPos.x, y: e.y - pointerStartPos.y };
        props.node.position.x = nodeStartPos.x + delta.x;
        props.node.position.y = nodeStartPos.y + delta.y;
        nodeElement.value.style.left = nodeStartPos.x + delta.x + "px";
        nodeElement.value.style.top = nodeStartPos.y + delta.y + "px";
    }
};

function ondragend(e) {
    const x = parseInt(nodeElement.value.style.left);
    const y = parseInt(nodeElement.value.style.top);
    emit("move");
};

function ondragover(e) {
    e.preventDefault();
};

</script>
<template>
    <div class="node btn" draggable="true" @dragstart="ondragstart" @drag="ondrag" @dragend="ondragend" @dragover="ondragover"
        ref="nodeElement">
        <Title :title="node.title" />
        <Element v-for="element in node.elements" :key="element" :element="element" />
    </div>
</template>
<style>
.node {
    position: absolute;
    border: 1px solid #282828;
    border-radius: .2em;
    background-color: #181818;
    max-width: 256px;
    box-shadow: 0 2px 4px #0002;
}

@media (prefers-color-scheme: light) {
    .node {
        border: 1px solid #e2e2e2;
        background-color: #fefefe;
    }
}
</style>
