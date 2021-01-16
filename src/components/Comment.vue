<template>
  <li class="list-item">
    <div>
      <p>
        <strong>{{ email }}</strong>
      </p>
      <small>{{ body }}</small>
    </div>
  </li>
</template>

<script>
export default {
  props: {
    email: String,
    body: String,
  },
};
</script>

<style>
</style>