<template>
  <div class="wrapper-login">
    <FormLogin/>
  </div>
</template>

<script>
import FormLogin from '@/components/FormLogin'

export default {
  name: 'Login',
  components: {
    FormLogin
  }
}
</script>

<style lang="scss">
  .wrapper-login {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
