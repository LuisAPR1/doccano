<template>
  <v-card>
    <v-card-title>
      <span class="headline">Criar Cliente</span>
    </v-card-title>
    <v-card-text>
      <v-form ref="form" @submit.prevent="submitClient">
        <v-text-field
          v-model="clientName"
          label="Nome do Cliente"
          :rules="[v => !!v || 'O nome é obrigatório']"
        />
        <v-text-field
          v-model="clientEmail"
          label="E-mail"
          :rules="[
            v => !!v || 'O e-mail é obrigatório',
            v => /.+@.+\..+/.test(v) || 'E-mail inválido'
          ]"
        />
        <v-text-field
          v-model="clientPhone"
          label="Telefone"
          :rules="[v => !!v || 'O telefone é obrigatório']"
        />
        <v-text-field
          v-model="clientAddress"
          label="Endereço"
          :rules="[v => !!v || 'O endereço é obrigatório']"
        />
        <!-- Adicione outros campos necessários aqui -->
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-spacer />
      <v-btn color="primary" @click="submitClient">
        Criar Cliente
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  layout: 'projects',
  data() {
    return {
      clientName: '',
      clientEmail: '',
      clientPhone: '',
      clientAddress: ''
    }
  },
  methods: {
    submitClient() {
      // Exemplo de chamada à API para criação de um cliente com os novos campos
      this.$axios
        .post(`/api/projects/${this.$route.params.id}/clients`, {
          name: this.clientName,
          email: this.clientEmail,
          phone: this.clientPhone,
          address: this.clientAddress
        })
        .then(() => {
          this.$toast.success('Cliente criado com sucesso!')
          this.$router.push({ path: `/projects/${this.$route.params.id}/clients` })
        })
        .catch(error => {
          this.$toast.error('Erro ao criar cliente.')
          console.error(error)
        })
    }
  }
})
</script>

<style scoped>
.v-card {
  margin: 20px;
}
</style>
