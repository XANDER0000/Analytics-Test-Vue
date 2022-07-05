<template>
  <div class="container">
     <div class="header">
      <h1>LeadHit</h1>
    </div>
    <form
     method="GET"
     class="main__form"
     action=""
     @submit="checkForm">
      <label for="siteId">Id Сайта</label>
      <input v-model="siteId" id="siteId" type="text">
      <button class="btn"><span>Войти</span></button>
    </form>
  </div>
  <MainError error="errors" v-if="errors.length"/>
</template>

<script>
import MainError from '@/components/MainError.vue'

export default {
  name: 'HelloWorld',

  components: {
    MainError
  },

  data: () => ({
    validation: [],
    siteId: '',
    errors: [],
    LeadhitSiteId: null
  }),

  methods: {
    checkForm (e) {
      if (this.siteId.length !== 24) {
        this.errors.push('id сайта должен содержать 24 символа')
      } else {
        this.errors = []
        fetch('https://track-api.leadhit.io/client/test_auth')
        .then(function(response) {
          return response.json()
        })
        .then(data => this.validation = data.detail[0].loc[0])

        .catch(function(error) {
          console.log(error)
        })

        this.saveLocalStorage()
        this.$router.push("/analytics");
      }
    },

    saveLocalStorage() {
      const parsed = JSON.stringify(this.siteId);
      localStorage.setItem('leadhit-site-id', parsed);
    }
  },

  created () {

  },

  watch: {
    siteId: function () {
      this.errors = []
    }
  },

  computed: {
  }
}
</script>

<style scoped lang="scss">
.main__form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  width: min-content;
  margin: 0 auto;

  input {
    padding: 8px 2px 8px 8px;
    font-size: 15px;
    color: #000;
    outline: none;
    border: 1px #006DFE solid;
  }
}
</style>
