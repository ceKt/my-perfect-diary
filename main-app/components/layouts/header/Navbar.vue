<template>
<div>
    <nuxt-link to="/">
        <Logo />
    </nuxt-link>
</div>
</template>

<script>

export default {
  name: 'Navbar',
  components: {
      Logo: () => import("~/components/layouts/header/Logo.vue"),
  }
}
</script>

