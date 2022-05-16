<template>
<div id="main_app">
    <header><LayoutsHeader /></header>
    <main>
      <div id="main_contents">
        <Scheduler />
        <Diary />
      </div>
    </main>
    <footer><LayoutsFooter /></footer>
</div>
</template>

<script>
export default {
  name: 'IndexPage',
  components:{
    Scheduler: () => import("~/components/contents/scheduler/index.vue"),
    Diary: () => import("~/components/contents/diary/index.vue"),
  }
}
</script>

<style>
body {
  background: #FFFFFF;
}
#main_app {
  margin-top: 10px;
  margin-right: auto;
}
#main_contents {
  display: flex;
  justify-content: center;
  margin-top: 10px;
}
footer {
  background: #FFFFFF;
}
</style>
