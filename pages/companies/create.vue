<template>
  <section class="py-[200px] flex flex-col items-center justify-center px-4">
    <div class="txt-[32px] font-semibold text-dark mb-4">Create Companies</div>
    <form class="w-full card" @submit.prevent="createCompany">
      <div class="form-group">
        <label for="name" class="text-grey">Company Name</label>
        <input type="text" id="name" class="input-field" v-model="company.name" />
      </div>
      <button type="submit" class="w-full btn btn-primary mt-[14px]">
          Continue
      </button>
    </form>
  </section>
</template>

<script>
export default {
  middleware: 'auth',
  data() {
    return {
      company: {
        name: ''
      }
    }
  },

  async fetch() {
    this.companies = await this.$axios.get('/company');
  },

  methods: {
    createCompany() {
      try {
        this.$axios.post('/company', this.company)
          .then(response => {
            this.$router.push({
              name: 'companies-id',
              params: {
                id: response.data.data.id
              }
            })
          })
      } catch (error) {
        console.log(error);
      }
    }
  }
}
</script>
