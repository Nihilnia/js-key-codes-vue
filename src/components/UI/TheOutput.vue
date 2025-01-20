<template>
  <div>
    <h5>{{ label }}: {{ result }}</h5>
  </div>
</template>

<script>
export default {
  props: ["label", "result"],
  data() {
    return {};
  },
};
</script>

<style scoped>
div {
  padding: 5px 30px;
  border: 1px solid rgba(255, 255, 255, 0.44);
  margin-top: 20px;
}

div:hover {
  transform: scale(1.04);
}

h5 {
  margin: 0;
  padding: 0;
}
</style>
