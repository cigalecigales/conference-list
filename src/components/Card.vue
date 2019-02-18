<template>
  <div class="card">
    <div class="name">
      <a :href="data.url" target="_blank">
        {{ data.name }}
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    data: Object
  }
}
</script>

<style scoped>
.card {
  background: #ffffff;
  border: 1px solid #dddddd;
  border-radius: 3px;
  padding: 10px;
}
</style>
