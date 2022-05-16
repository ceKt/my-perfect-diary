<template>
<div id="scheduler">
    <div id="createTaskModal">
        <div id="setTime">
            <div id="setStartTime">
                開始時刻：<input type="time" v-model="inputStartTime">
            </div>
            <div id="setEndTime">
                終了時刻：<input type="time" v-model="inputEndTime">
            </div>
        </div>
        <table id="inputTable">
            <tr><td class="w20">title：</td><td class="w70"><input id="setDescription" type="text" v-model="inputTitle"></td></tr>
            <tr><td class="w20">詳細：</td><td class="w70"><input id="setAttachedUrl" type="text" v-model="inputDescription"></td></tr>
        </table>
        <div id="setButton">
            <button id="addButton" v-on:click="addTask">追加</button>
        </div>
    </div>
    <div id="scheduler_main">
        <div class="stime"><p>3:00a.m.</p></div>
        <div class="stime"><p>4:00a.m.</p></div>
        <div class="stime"><p>5:00a.m.</p></div>
        <div class="stime"><p>6:00a.m.</p></div>
        <div class="stime"><p>7:00a.m.</p></div>
        <div class="stime"><p>8:00a.m.</p></div>
        <div class="stime"><p>9:00a.m.</p></div>
        <div class="stime"><p>10:00a.m.</p></div>
        <div class="stime"><p>11:00a.m.</p></div>
        <div class="stime"><p>noon</p></div>
        <div class="stime"><p>1:00p.m.</p></div>
        <div class="stime"><p>2:00p.m.</p></div>
        <div class="stime"><p>3:00p.m.</p></div>
        <div class="stime"><p>4:00p.m.</p></div>
        <div class="stime"><p>5:00p.m.</p></div>
        <div class="stime"><p>6:00p.m.</p></div>
        <div class="stime"><p>7:00p.m.</p></div>
        <div class="stime"><p>8:00p.m.</p></div>
        <div class="stime"><p>9:00p.m.</p></div>
        <div class="stime"><p>10:00p.m.</p></div>
        <div class="stime"><p>11:00p.m.</p></div>
        <div class="stime"><p>12:00p.m.</p></div>
        <div class="stime"><p>0:00a.m.</p></div>
        <div class="stime"><p>1:00a.m.</p></div>
        <div class="stime"><p>2:00a.m.</p></div>
        <div class="stime"><p>3:00a.m.</p></div>
        <div id="scheduler_tasks">
            <Task v-for="(task,index) in scheduler_tasks" :key="index" :taskData="task" :positionData="taskPosition(task)" />
        </div>

    </div>
</div>
</template>

<script>
    export default {
        name: "Scheduler",

        data: function() {
            return {
                scheduler_tasks: [
                    {
                        date: "yyyy-mm-dd",
                        start: "3:10:00",
                        end: "2:20:00",
                        title: "test",
                        description: "これはテストでしゅ1。",
                    },
                    {
                        date: "yyyy-mm-dd",
                        start: "15:00:00",
                        end: "16:20:00",
                        title: "test2",
                        description: "これはテストでしゅ2。",
                    },
                    {
                        date: "yyyy-mm-dd",
                        start: "19:20:00",
                        end: "20:20:00",
                        title: "test3",
                        description: "これはテストでしゅ3。",
                    }
                ],
                inputStartTime: "",
                inputEndTime: "",
                inputTitle: "",
                inputDescription: "",
            }
        },

        methods: {
            addTask: function () {
                if(this.inputStartTime && this.inputEndTime && this.inputTitle){
                    this.scheduler_tasks.push({
                    date: "yyyy-mm-dd",
                    start: this.inputStartTime,
                    end: this.inputEndTime,
                    title: this.inputTitle,
                    description: this.inputDescription,
                });
                }
                
                console.log(this.scheduler_tasks);
            },
            textToTime: function(datetext) {
                var datetime = datetext.split(':');
                return {
                    hour: Number(datetime[0]),
                    min: Number(datetime[1]),
                    sec: Number(datetime[2]),
                }
            },
            taskPosition: function(task) {
                var start = this.textToTime(task.start);
                var end = this.textToTime(task.end);
                if(start.hour<3)start.hour+=25;
                if(end.hour<3)end.hour+=25;
                var top = (start.hour-2+start.min/60)*6;
                var height = ((end.hour-start.hour)+(end.min-start.min)/60)*6;
                return {
                    top: top,
                    left: 0,
                    height: height,
                    width: 30,
                }
            }
        },

        components: {
            Task: () => import("~/components/contents/scheduler/Task.vue"),
        },
        
    }
</script>

<style>
#scheduler {
    width: 480px;
    height: 720px;
    background-color: #FFFFFF;
    margin-left: auto;
    border-radius: 1rem;
}


#createTaskModal {
    width: 95%;
    height: 18%;
    margin: auto;
    background-color: #FFFFFF;
    box-shadow: 1px 1px 2px;
}

#createTaskModal #setTime {
    display: flex;
}

#createTaskModal #setStartTime {
    margin: auto;
}
#createTaskModal #setEndTime {
    margin: auto;
}
#createTaskModal #setDescription {
    width: 100%;
}
#createTaskModal #setAttachedUrl{
    width: 100%;
}

#createTaskModal table{
    margin:auto;
}
#createTaskModal .w20 {
    width: 20%;
}
#createTaskModal .w70 {
    width: 70%;
}

#setButton {
    display: flex;
    justify-content: flex-end;
}
#createTaskModal #addButton {
    margin-right: 5px;
}


#scheduler_main {
    position: relative;
    width: 100%;
    height: 85%;
    margin-top: 1%;
    overflow: auto;
}
#scheduler_main::-webkit-scrollbar{
    display: none;
}

.stime {
    position: relative;
    width: 90%;
    height: 6%;
    margin: auto;
    border-bottom-style: solid;
    border-bottom-width: 1px;
    border-bottom-color: #B0B0B0;
}
.stime p{
    position: absolute;
    bottom: 0;
    margin: 0;
}

#scheduler_tasks {
    width: 70%;
    height: 100%;
    position: absolute;
    top: 0%;
    left: 30%;
}

</style>