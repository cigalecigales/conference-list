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
  background: #008B8B;
  color: #ffffff;
  padding: 3px 8px;
  border-radius: 8px;
  margin-left: 5px;
  margin-right: 5px;
}
</style>
