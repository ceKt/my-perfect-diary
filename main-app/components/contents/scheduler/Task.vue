<template>
    <div class="scheduler_task" v-bind:style="{
        top: positionTop,
        left: positionLeft,
        height: positionHeight,
        width: positionWidth,
        background: taskData.color,
    }"
    v-on:click="showDetail">
        <div class="simpleTask" v-if="!isOpen">
            {{taskData.title}}
        </div>
        <div class="detailTask" v-else>
            <p>時間：{{taskData.start}}～{{taskData.end}}</p>
            <p>タイトル：{{taskData.title}}</p>
            <p>詳細：{{taskData.description}}</p>
            <button v-on:click="deleteTask">削除</button>
        </div>
    </div>
</template>

<script>
export default {

    mounted: function() {
        window.addEventListener('click', this._onBlurHandler = (event) => {
            if(!event.target.closest('.scheduler_task')) {
                this.isOpen = false;
                this.positionHeight = this.taskData.positionData.height+'%';
                this.positionWidth = this.taskData.positionData.width+'%';
            }
        });
    },
    
    beforeUpdate: function(){
        this.positionTop = this.taskData.positionData.top+'%';
        this.positionLeft = this.taskData.positionData.left+'%';
    },

    beforeDestroy: function() {
        window.removeEventListener('click', this._onBlurHandler);
    },

    methods: {
        showDetail: function(){
            this.isOpen = true;
            this.positionHeight = "auto";
            this.positionWidth = '100%';
        },
        closeDetail: function(){
            this.isOpen = false;
            this.positionHeight = this.taskData.positionData.height+'%';
            this.positionWidth = this.taskData.positionData.width+'%';
        },
        deleteTask: function(){
            this.$emit("deleteTask", this.taskData);
        },
    },

    beforeDestroy: function(){
    },

    props: {
        taskData: {
            type: Object,
            required: true,
        },
    },

    data: function() {
        return {
           isOpen: false, 
           positionTop: this.taskData.positionData.top+'%',
           positionLeft: this.taskData.positionData.left+'%',
           positionHeight: this.taskData.positionData.height+'%',
           positionWidth: this.taskData.positionData.width+'%',
        }
    },
}
</script>

<style>
.scheduler_task {
    position: absolute;
    margin: 0;
    background: #0FD0AA;
    border-radius: 0.5rem;
    border: 0.3px solid #DDDDDD;
    box-shadow: 2px 2px #000000;
}
</style>