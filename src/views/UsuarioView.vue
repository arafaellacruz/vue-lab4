<template>
  <div>
    <p>
      {{ nome }}
    </p>
    <p>
      <label id="labelUsuario" for="usuario">Nome: </label>
      <input id="usuario" v-model="nome" />
    </p>

    <p>
      <label id="labelSenha" for="senha">Senha: </label>
      <input id="senha" type="password" v-model="senha" />
    </p>

    <p v-if="senha.length < 5">A senha deve ter pelo menos 5 caracteres.</p>
    <p v-else>A senha atende aos requisitos.</p>

    <button @click="cadastrarUsuario">Cadastrar</button>

    <table>
      <thead>
        <tr>
          <th>Nome</th>
          <th>Senha</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="usuario in usuarios" :key="usuario.id">
          <td>{{ usuario.id }}</td>
          <td>{{ usuario.nome }}</td>
          <td>{{ usuario.senha }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

interface usuario {
  id?: number
  nome: string
  senha: string
}

const nome = ref<string>('Hello World!')
const senha = ref<string>('12345')
const cont = ref<number>(3)

const usuarios = ref<usuario[]>([
  {
    id: 1,
    nome: 'admin',
    senha: 'admin',
  },
  {
    id: 2,
    nome: 'teste',
    senha: '123',
  },
])

function cadastrarUsuario() {
  usuarios.value.push({
    id: usuarios.value.length + 1,
    nome: nome.value,
    senha: senha.value,
  })

  nome.value = ''
  senha.value = ''
}
</script>
