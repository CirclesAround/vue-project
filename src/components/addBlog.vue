<template>
  <div class="add-blog">
    <h2>添加博客</h2>
    <form v-if="!submmited">
      <label>博客标题</label>
      <input class="choose" type="text" v-model="blog.title" required>

      <label>博客内容</label>
      <textarea name v-model="blog.content"></textarea>

      <div class="checkboxes">
        <template v-for="(item, index) in blog.list">
          <label :for="index">{{item}}</label>
          <input :id="index" type="checkbox" v-bind:value="item" v-model="blog.categories">
        </template>
      </div>
      <p>作者：</p>
      <select v-model="blog.chooseAuthor">
        <option v-for="author in blog.authors" :value="author">{{author}}</option>
      </select>
      <button @click.prevent="post">添加博客</button>
    </form>

    <div v-if="submmited">
      <h3>您的博客发布成功</h3>
    </div>

    <div class="preview">
      <h3>博客总览：</h3>
      <p>博客标题： {{blog.title}}</p>
      <p>博客内容：</p>
      <p>{{blog.content}}</p>
      <p>博客分类:</p>
      <ul>
        <li v-for="categories in blog.categories">{{categories}}</li>
      </ul>
      <P>作者: {{blog.chooseAuthor}}</P>
    </div>
    <div class="test">
      <p>按很多卡接收到</p>
      <p>测试</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "add-blog",
  data() {
    return {
      blog: {
        title: "",
        content: "",
        list: ["vue.js", "node.js", "react.js", "angular4"],
        categories: [],
        authors: ["vision", "jack", "威斯贝斯"],
        chooseAuthor: ""
      },
      submmited: false
    };
  },
  methods: {
    post: function() {
      this.$http
        .post("http://jsonplaceholder.typicode.com/posts", {
          title: this.blog.title,
          body: this.blog.content,
          userId: 1
        })
        .then(function(res) {
          console.log(res);
          this.submmited = true;
        });
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
html {
  font-size: 13.33vw;
}
form {
  display: flex;
  flex-direction: column;
  align-content: center;
  justify-content: center;
}
.choose,
textarea {
  border: 1px solid #ccc;
  border-radius: 2px;
  padding: 0 0.2rem;
  width: 6rem;
  font-size: 0.3rem;
  margin: 0.2rem auto;
}
textarea {
  resize: none;
}
.checkboxes {
  display: flex;
  align-items: center;
}
select {
  width: 3rem;
}
button {
  width: 2rem;
  background-color: #ff7c3e;
  color: #fff;
  font-size: 0.34rem;
}
.test {
  p {
    &:first-child {
      color: #ff7c3e;
      font-size: 0.32rem;
    }
    &:last-child {
      color: #3a3a3a;
      font-size: 0.36rem;
    }
  }
}
</style>
