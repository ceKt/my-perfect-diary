<template>
<div class="diary">
    <p>日記</p>
    <textarea id="inputDiary"></textarea>
    <div id="saveDiary">
        <button id="saveDiaryButton" v-on:click="">日記更新</button>
    </div>
</div>
</template>

<style>
.diary {
    width: 480px;
    height: 720px;
    margin-right: auto;
    border-radius: 1rem;
    text-align: center;
}
#inputDiary {
    width: 95%;
    height: 90%;
    border-radius: 1rem;
    font-size: 15pt;
    line-height: 31px;
    padding: 31px;

    /* 罫線描画（各ブラウザ対応）*/
    background-image: -webkit-linear-gradient(left, white 10px, transparent 10px), -webkit-linear-gradient(right, white 10px, transparent 10px), -webkit-linear-gradient(white 30px, #ccc 30px, #ccc 31px, white 31px);
    background-size: 100% 100%, 100% 100%, 100% 31px;
    border: none;
}

#saveDiary {
    display: flex;
    justify-content: flex-end;
}
#saveDiaryButton {
    margin-right: 5px;
}

</style>

