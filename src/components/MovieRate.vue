<template>
  <p>
    <span class="title">{{ title }}</span> directed by {{ director }} from
    {{ year }} was rated with <span class="rate">{{ rate }}</span>
    {{ rate > 1 ? "points" : "point" }}.
  </p>
</template>

<script>
export default {
  props: ["title", "director", "year", "rate"],
};
</script>

<style scoped>
p {
  font-size: 1.5rem;
  margin: 10px;
  text-align: center;
}

span.title {
  color: #153d36;
}

span.rate {
  color: #ffe562;
}
</style>