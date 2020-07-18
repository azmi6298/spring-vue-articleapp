<template>
  <div>
    <ArticleComponent 
      :id="$route.params.id"
    />
  </div>
</template>

<script>
import {mapActions, mapGetters} from 'vuex'
import ArticleComponent from '../components/ArticleComponent'
export default {
  name: 'EditArticle',
  components: {
    ArticleComponent
  },
  created() {
    this.getCurrentArticle(this.$route.params.id)
  },
  computed: {
    ...mapGetters(['currentArticle']),
  },
  methods: {
    ...mapActions(['getCurrentArticle']),
  }
}
</script>