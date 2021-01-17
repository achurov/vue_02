<template>
  <form class="card card-w30" v-on:keyup.enter="add" @submit.prevent="add">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" rows="3" v-model.trim="value"></textarea>
    </div>

    <button class="btn primary" :disabled="addDisabled">Добавить</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      type: "title",
      value: "",
    };
  },
  computed: {
    addDisabled: function () {
      return this.value.length < 4;
    },
  },
  emits: ["add"],
  methods: {
    add() {
      this.$emit("add", {
        type: this.type,
        value: this.value,
      });

      this.type = "title";
      this.value = "";
    },
  },
};
</script>

<style>
</style>