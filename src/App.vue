<template>
  <div class="container column">
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

    <div class="card card-w70">
      <h3 v-if="data.length === 0">
        Добавьте первый блок, чтобы увидеть результат
      </h3>

      <component
        v-for="item in data"
        :key="item"
        v-bind:is="item.type"
        :value="item.value"
      ></component>
    </div>
  </div>
  
  <div class="container">
    <p>
      <button class="btn primary" @click="loadComments">
        Загрузить комментарии
      </button>
    </p>
    <div class="loader" v-if="loader"></div>
    <div class="card" v-if="commentsShow">
      <h2>Комментарии</h2>
      <ul class="list">
        <comment
          v-for="item in comments"
          :key="item"
          :email="item.email"
          :body="item.body"
        ></comment>
      </ul>
    </div>
  </div>
</template>

<script>
import Avatar from "./components/Avatar.vue";
import Comment from "./components/Comment.vue";
import Subtitle from "./components/Subtitle.vue";
import Text from "./components/Text.vue";
import Title from "./components/Title.vue";

export default {
  data() {
    return {
      type: "",
      value: "",
      data: [],
      comments: [],
      loader: false,
    };
  },
  mounted() {
    this.formReset();
  },
  computed: {
    addDisabled: function () {
      return this.value.length < 4;
    },
    commentsShow: function () {
      return this.comments.length > 0;
    },
  },
  methods: {
    formReset() {
      console.log(21432);
      this.type = "title";
      this.value = "";
    },
    add() {
      this.data.push({
        type: this.type,
        value: this.value,
      });

      this.formReset();
    },
    async loadComments() {
      this.loader = true;
      const response = await fetch(
        "https://jsonplaceholder.typicode.com/comments?_limit=42",
        {
          method: "GET",
        }
      );

      this.loader = false;
      this.comments = await response.json();
    },
  },
  components: {
    title: Title,
    avatar: Avatar,
    subtitle: Subtitle,
    text: Text,
    comment: Comment,
  },
};
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
