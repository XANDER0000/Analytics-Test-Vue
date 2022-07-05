<template>
  <div class="error">
    <div class="error__content">
      id сайта должен содержать 24 символа
    </div>
  </div>
</template>

<script>
export default {
  name: 'MainError',

  props: {
    error: {
      String
    }
  }
}
</script>

<style scoped lang="scss">
.error {
  position: fixed;
  left: 0;
  bottom: 0;
  padding: 10px 15px;
  max-width: 500px;
  border-radius: 3px;
  background: rgba(255, 0, 0, 0.264);
}
</style>
