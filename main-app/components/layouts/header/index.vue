<template>
    <Navbar />
</template>

<script>

export default {
  name: 'HeaderIndex',
  components: {
      Navbar: () => import("~/components/layouts/header/Navbar.vue"), 
  }
}
</script>