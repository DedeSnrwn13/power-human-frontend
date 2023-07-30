<template>
  <section class="py-[200px] flex flex-col items-center justify-center px-4">
    <div class="txt-[32px] font-semibold text-dark mb-4">Select Companies</div>
    <div class="w-full card">
      <div class="form-group">
        <label for="companies" class="text-grey">Companies</label>
        <p v-if="$fetchState.pending">Fetching Companies...</p>
        <select v-else name="companies" id="companies" class="appearance-none input-field form-icon-chevron_down" v-model="selectedCompany">
          <option :value="company.id" v-for="(company, index) in companies.data.data.data" :key="index">
            {{ company.name }}
          </option>
        </select>
      </div>
      <button @click="openCompany()" type="button" class="w-full btn btn-primary mt-[14px]">
        Continue
      </button>
      <div class="text-center">or</div>
      <NuxtLink :to="{ name: 'companies-create' }" class="w-full btn btn-white border-2">
        Create New Company
      </NuxtLink>
    </div>
  </section>
</template>

<script>
export default {
  middleware: 'auth',
  data() {
    return {
      companies: [],
      selectedCompany: ''
    }
  },

  async fetch() {
    this.companies = await this.$axios.get('/company');
  },

  methods: {
    openCompany() {
      this.$router.push({
        name: 'companies-id',
        params: {
          id: this.selectedCompany
        }
      });
    }
  }
}
</script>
