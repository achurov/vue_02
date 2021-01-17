<template>
  <div class="card card-w70">
    <h3 v-if="data.length === 0">
      Добавьте первый блок, чтобы увидеть результат
    </h3>

    <component
      v-for="item in data"
      :key="item"
      :is="item.type"
      :value="item.value"
    ></component>
  </div>
</template>

<script>
import Subtitle from "./Subtitle.vue";
import Text from "./Text.vue";
import Title from "./Title.vue";
import Avatar from "./Avatar.vue";

export default {
  inject: ["data"],
  components: {
    title: Title,
    avatar: Avatar,
    subtitle: Subtitle,
    text: Text,
  },
};
</script>

<style>
</style>