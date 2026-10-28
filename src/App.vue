<template>
  <main>
    <h1>Buscador de Perfis GitHub</h1>

    <p>
      Digite o nome de usuário para encontrar um perfil.
    </p>

    <div>

       <!-- @keyup.enter permite pesquisar pressionando enter-->
      <input
        type="text"
        v-model="username"
        placeholder="Digite um usuário do GitHub"
        @keyup.enter="buscarPerfil"
      >

      <button @click="buscarPerfil">
        Buscar
      </button>
    </div>

    <!--{{  }} interpolação permite exibir na página o valor de uma variável-->
    <p>Você digitou: {{ username }}</p>

    <p v-if="carregando">
      Buscando perfil...
    </p>

    <p v-else-if="erro">
      {{ erro }}
    </p>

    <div v-if="perfil">
      <img
        :src="perfil.avatar_url"
        alt="Foto do perfil"
        width="120"
      >

      <h2>{{ perfil.name || perfil.login }}</h2>

      <p v-if="perfil.bio">{{ perfil.bio }}</p>

      <p>Seguidores: {{ perfil.followers }}</p>

      <p>Repositórios públicos: {{ perfil.public_repos }}</p>

      <a
       :href="perfil.html_url" target="_blank" rel="noopener noreferrer"
      >
        Ver perfil no GitHub
      </a>

    </div>
  </main>
</template>


<script setup>

    import { ref } from 'vue'

    const username = ref('')
    const perfil = ref(null)
    const carregando = ref(false)
    const erro = ref('')

    async function buscarPerfil() {

    //verifica se o campo está vazio
  
    if (!username.value.trim()) {
    erro.value = 'Digite um nome de usuário.'
    perfil.value = null
    return
   }
  
   //Prepara a busca
   carregando.value = true
   erro.value = ''
   perfil.value = null

   try {

    //Faz a requisição
    const resposta = await fetch(
      `https://api.github.com/users/${username.value.trim()}`
    )

    // Se usuário for encontrado
    if (!resposta.ok) {

      //Se usuário der como inexistente 
      if (resposta.status === 404) {
        throw new Error('Usuário não encontrado.')
      }

      throw new Error('Não foi possível buscar o perfil.')
    }

    const dados = await resposta.json()
    perfil.value = dados
  } catch (error) {
    erro.value = error.message

  // Desliga o carregamento mesmo com erro  
  } finally {
    carregando.value = false
  }

}
    
</script>

<style>


* {
  box-sizing: border-box;
}

body {
  margin: 0;
  min-height: 100vh;
  font-family: 'Segoe UI', Arial, sans-serif;
  color: #f5f3ff;

  background:
    linear-gradient(rgba(5, 7, 24, 0.75), rgba(18, 10, 45, 0.75)),
    url('./assets/github-bg.png') center / cover no-repeat fixed;
}

/* Centraliza o conteúdo na tela */
#app {
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px;
}

/* Card de vidro */
main {
  width: 100%;
  max-width: 580px;
  margin: 0;
  padding: 38px 32px;
  text-align: center;

  background: rgba(13, 16, 40, 0.78);
  backdrop-filter: blur(22px);
  -webkit-backdrop-filter: blur(22px);

  border: 1px solid rgba(173, 151, 255, 0.25);
  border-radius: 24px;

  box-shadow: 0 24px 80px rgba(0, 0, 0, 0.45),
              0 0 35px rgba(110, 65, 255, 0.12);
}

h1 {
  margin-top: 0;
  color: #fff;
  font-size: 30px;
}

main > p {
  color: #c3c5df;
  line-height: 1.6;
}

/* Pesquisa */
main > div:first-of-type {
  display: flex;
  gap: 10px;
  margin-top: 26px;
}

input {
  flex: 1;
  min-width: 0;
  padding: 14px;
  color: white;
  background: rgba(255, 255, 255, 0.06);
  border: 1px solid rgba(176, 163, 255, 0.3);
  border-radius: 12px;
  outline: none;
}

input::placeholder {
  color: #9296b8;
}

input:focus {
  border-color: #9b7bff;
}

button {
  padding: 14px 20px;
  border: none;
  border-radius: 12px;
  background: linear-gradient(135deg, #8b5cf6, #5267f5);
  color: white;
  font-weight: 600;
  cursor: pointer;
}

button:hover {
  filter: brightness(1.15);
}

/* Perfil */
main > div:last-child {
  margin-top: 28px;
  padding: 24px 18px;
  background: rgba(255, 255, 255, 0.045);
  border: 1px solid rgba(164, 148, 255, 0.18);
  border-radius: 18px;
}

img {
  width: 112px;
  height: 112px;
  object-fit: cover;
  border-radius: 50%;
  margin-top: 8px;
  border: 3px solid #a78bfa;
  box-shadow: 0 0 28px rgba(124, 92, 255, 0.25);
}

h2 {
  color: white;
}

main > div:last-child p {
  color: #c9cbe2;
  overflow-wrap: anywhere;
}

a {
  display: inline-block;
  margin-top: 12px;
  padding: 10px 16px;
  color: #d9ccff;
  text-decoration: none;
  border: 1px solid rgba(167, 139, 250, 0.35);
  border-radius: 10px;
}

a:hover {
  background: rgba(139, 92, 246, 0.15);
}

/* Celular */
@media (max-width: 520px) {
  #app {
    padding: 16px;
  }

  main {
    padding: 28px 20px;
  }

  main > div:first-of-type {
    flex-direction: column;
  }

  button {
    width: 100%;
  }
}

</style>