<template>
  <div>
    <h1>{{ formTitle }}</h1>
    <b-form @submit.prevent="onSubmit">
      <b-form-group id="input-group-2" label="Title:">
        <b-form-input
          :value="title"
          @input="updateTitle"
          placeholder="Enter Title"
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-2" label="Content:">
        <b-form-textarea
          :value="content"
          @input="updateContent"
          placeholder="Enter Content"
        ></b-form-textarea>
      </b-form-group>
      <b-form-group id="input-group-2" label="Published:" v-if="this.$route.params.id != undefined">
        <b-form-input
          :value="published"
          @input="updatePublished"
          placeholder="Enter Published Date"
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary" class="mr-4">Save</b-button>
      <b-button type="reset" variant="danger" v-if="this.$route.params.id != undefined" @click="removeArticle">Delete</b-button>
    </b-form>
  </div>
</template>

<script>
import {mapActions} from 'vuex'
export default {
  name: "ArticleComponent",
  props: ['id', 'title', 'content', 'published'],
  data() {
    return {
      article: {
        id: '',
        title: '',
        content: '',
        published: ''
      }
    }
  },
  created() {
    this.$set(this.article, 'id', this.id)
    this.$set(this.article, 'title', this.title)
    this.$set(this.article, 'content', this.content)
    this.$set(this.article, 'published', this.published)
  },
  computed: {
    formTitle() {
      if(this.id  != undefined) {
        return "Update Article"
      } else {
        return "Create New Article"
      }
    },
  },
  methods: {
    ...mapActions(['addArticle', 'updateArticle', 'deleteArticle', 'getCurrentArticle']),
    updateTitle(value) {
      this.article.title = value
    },
    updateContent(value) {
      this.article.content = value
    },
    updatePublished(value) {
      this.article.published = value
    },
    saveArticle() {
      this.addArticle(this.article)
      this.$router.push({ name: 'home' })
    },
    changeArticle() {
      this.updateArticle(this.article)
      this.$router.push({ name: 'home' })
    },
    removeArticle() {
      this.deleteArticle(this.id)
      this.$router.push({ name: 'home' })
    },
    onSubmit() {
      if(this.$route.params.id == undefined) {
        this.saveArticle()
      } else {
        console.log(this.article)
        this.changeArticle(this.article)
      }
    },
  },
}
</script>