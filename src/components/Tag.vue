<template>
  <div class="tag">
    {{ tag }}
  </div>
</template>

<script>
export default {
  name: 'Tag',
  props: {
    tag: {
      type: String
    }
  }
}
</script>

<style scoped>
.tag {
  display: inline-block;
  background: #394989;
  color: #ffffff;
  padding: 3px 12px;
  border-radius: 5px;
  margin-left: 5px;
  margin-right: 5px;
}
</style>
