<template>
  <router-view/>
</template>

<script>
export default {
  beforeMount() {
    if (document.cookie.indexOf('log_c') != '-1') {
      this.$router.push('/')
    }
  }
}
</script>

