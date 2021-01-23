<template>
  <div class="container column">
    
    <form class="card card-w30">
      <div class="form-control">
        <label for="type">Тип блока</label>
        <select id="type" v-model="option">
          <option value="title">Заголовок</option>
          <option value="subtitle">Подзаголовок</option>
          <option value="avatar">Аватар</option>
          <option value="text">Текст</option>
        </select>
      </div>

      <div class="form-control">
        <label for="value">Значение</label>
        <textarea id="value" rows="3" v-model.trim="textValue"></textarea>
      </div>

      <button class="btn primary" :disabled="textValue.length < 3" @click="addItem">Добавить</button>
    </form>

    <div class="card card-w70">

      <component
        v-for="(el, i) in compArr"
        :key='i'
        :is="el.name"
        v-bind="el.propsOb"
      />
      
      <h3 v-if="!compArr.length">Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <div class="container">
    <p>
      <button class="btn primary" 
        @click="loadComments"
        v-if="!commentsArr.length"
      >
        Загрузить комментарии
      </button>
    </p>
    <div class="card" v-if="commentsArr.length">
      <h2>Комментарии</h2>
      <ul class="list">
        <app-comment
          v-for="el in commentsArr"
          :key="el.id"
          :email="el.email"
          :body="el.body"
        />
      </ul>
    </div>
    <div class="loader" v-if="isLoading"></div>
  </div>
</template>

<script>
import AppTitle from './components/AppTitle.vue'
import AppSubtitle from './components/AppSubtitle.vue'
import AppAvatar from './components/AppAvatar.vue'
import AppText from './components/AppText.vue'
import AppComment from './components/AppComment.vue'
const axios = require('axios')

export default {
  components: {
    'app-title': AppTitle,
    'app-subtitle': AppSubtitle,
    'app-avatar': AppAvatar,
    'app-text': AppText,
    'app-comment': AppComment
  },
  data() {
    return {
      compArr: [],
      commentsArr: [],
      isLoading: false,
      option: 'title',
      textValue: ''
    }
  },
  methods:{
    async loadComments() {
      this.isLoading = true;
      try {
        const {data} = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42');
        this.commentsArr = data;
      } catch (error) {
        console.error(error);
      }
      this.isLoading = false;
    },

    addItem() {
      let ob = {};
      ob.name = 'app-' + this.option;
      ob.propsOb = {};
      ob.propsOb.text = this.textValue;
      this.compArr.push(ob);
      this.option = 'title';
      this.textValue = '';
    }
  }

}
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
