<template>
    <div class="scheduler_task" v-bind:style="{
        top: positionData.top+'%',
        left: positionData.left+'%',
        height: positionData.height+'%',
        width: positionData.width+'%',
    }">
    {{taskData.title}}
    </div>
</template>

<script>
export default {
    props: {
        taskData: {
            type: Object,
            required: true,
        },
        positionData: {
            type: Object,
            required: false,
        },
    },
}
</script>

<style>
.scheduler_task {
    position: absolute;
    margin: 0;
    background: #0FD0AA;
    border-radius: 0.5rem;
    border: 0.3px solid #FFFFFF;
    box-shadow: 2px 2px #000000;
}
</style>