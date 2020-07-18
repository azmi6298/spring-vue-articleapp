<template>
  <div>
    <FormComponent 
      :id="$route.params.id"
    />
  </div>
</template>

<script>
import {mapActions, mapGetters} from 'vuex'
import FormComponent from '../components/FormComponent'
export default {
  name: 'EditArticle',
  components: {
    FormComponent
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