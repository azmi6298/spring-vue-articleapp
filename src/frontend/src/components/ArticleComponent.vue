<template>
  <div>
    <h1>{{ formTitle }}</h1>
    <b-form @submit.prevent="onSubmit">
      <b-form-group id="input-group-2" label="Title:">
        <b-form-input
          v-model="article.title"
          placeholder="Enter Title"
        ></b-form-input>
      </b-form-group>
      <b-form-group id="input-group-2" label="Content:">
        <b-form-textarea
          v-model="article.content"
          placeholder="Enter Content"
        ></b-form-textarea>
      </b-form-group>
      <b-form-group id="input-group-2" label="Published:" v-if="this.$route.params.id != undefined">
        <b-form-input
          v-model="article.published"
          placeholder="Enter Published Date"
        ></b-form-input>
      </b-form-group>
      <b-button type="submit" variant="primary" class="mr-4">Save</b-button>
      <b-button type="reset" variant="danger" v-if="this.$route.params.id != undefined">Delete</b-button>
    </b-form>
  </div>
</template>

<script>
import {mapActions, mapGetters} from 'vuex'
export default {
  name: "ArticleComponent",
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
    if(this.$route.params.id !== undefined){
      
      this.getCurrentArticle(this.$route.params.id)
      // this.$set(this.article, 'title', this.currentArticle.title)
    }

      console.log(this.$route.params.id)
  },
  computed: {
    ...mapGetters(['currentArticle']),
    formTitle() {
      if(this.$route.params.id  != undefined) {
        return "Update Article"
      } else {
        return "Create New Article"
      }
    },
  },
  methods: {
    ...mapActions(['addArticle', 'updateArticle', 'deleteArticle', 'getCurrentArticle']),
    saveArticle() {
      this.addArticle(this.article)
    },
    changeArticle() {
      this.updateArticle(this.article)
    },
    removeArticle() {
      this.deleteArticle(this.article.id)
    },
    onSubmit() {
      if(this.$route.params.id != undefined) {
        this.saveArticle()
      } else {
        this.changeArticle()
      }
    },
  },
}
</script>