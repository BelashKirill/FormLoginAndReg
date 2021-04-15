<template>
  <div class="wrapper-login">
    <FormRegistration/>
  </div>
</template>

<script>
import FormRegistration from '@/components/FormRegistration'

export default {
  name: 'Registration',
  components: {
    FormRegistration
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