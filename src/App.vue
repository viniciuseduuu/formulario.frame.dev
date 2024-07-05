<script setup>
import { ref, computed, reactive } from 'vue'

const user = reactive({
  avatar: null,
  nome: '',
  sexo: '',
  email: '',
  senha: '',
  dataNasc: '',
  endereco: '',
  cidade: '',
  estado: '0',
  biography: '',
  hobbie: [],
  progLinguages: [],
  mainLinguage: '0'
})

const lingProg = ref('')

function addLinguage() {
  user.progLinguages.push(lingProg.value)
  lingProg.value = ''
}

const estados = [
  { sigla: 'AC', nome: 'Acre' },
  { sigla: 'AL', nome: 'Alagoas' },
  { sigla: 'AP', nome: 'Amapá' },
  { sigla: 'AM', nome: 'Amazonas' },
  { sigla: 'BA', nome: 'Bahia' },
  { sigla: 'CE', nome: 'Ceará' },
  { sigla: 'DF', nome: 'Distrito Federal' },
  { sigla: 'ES', nome: 'Espírito Santo' },
  { sigla: 'GO', nome: 'Goiás' },
  { sigla: 'MA', nome: 'Maranhão' },
  { sigla: 'MT', nome: 'Mato Grosso' },
  { sigla: 'MS', nome: 'Mato Grosso do Sul' },
  { sigla: 'MG', nome: 'Minas Gerais' },
  { sigla: 'PA', nome: 'Pará' },
  { sigla: 'PB', nome: 'Paraíba' },
  { sigla: 'PR', nome: 'Paraná' },
  { sigla: 'PE', nome: 'Pernambuco' },
  { sigla: 'PI', nome: 'Piauí' },
  { sigla: 'RJ', nome: 'Rio de Janeiro' },
  { sigla: 'RN', nome: 'Rio Grande do Norte' },
  { sigla: 'RS', nome: 'Rio Grande do Sul' },
  { sigla: 'RO', nome: 'Rondônia' },
  { sigla: 'RR', nome: 'Roraima' },
  { sigla: 'SC', nome: 'Santa Catarina' },
  { sigla: 'SP', nome: 'São Paulo' },
  { sigla: 'SE', nome: 'Sergipe' },
  { sigla: 'TO', nome: 'Tocantins' }
]

function enviarImagemperfil(e) {
  const target = e.target
  if (target && target.files) {
    const file = target.files[0]
    user.avatar = URL.createObjectURL(file)
  }
}

const enviado = ref(false)

function enviar() {
  enviado.value = true
}
function retornar() {
  enviado.value = false
}
</script>

<template>
  <head>
    <link
      href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.3/dist/css/bootstrap.min.css"
      rel="stylesheet"
      integrity="sha384-QWTKZyjpPEjISv5WaRU9OFeRpok6YctnYmDr5pNlyT2bRjXh0JMhjY6hW+ALEwIH"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div v-if="!enviado" class="validate">
      <form class="was-validate" @submit.prevent="enviar()">
        <div id="avatarUser">
          <img :src="user.avatar" />
          <label for="enviarFoto" style="cursor: pointer; color: rgb(110, 110, 250)"
            >Alterar Imagem</label
          >
          <input
            type="file"
            @change="enviarImagemperfil($event)"
            id="enviarFoto"
            style="opacity: 0; position: absolute; z-index: -1"
          />
        </div>
        <div id="firstForm">
          <input
            type="text"
            placeholder="Insira seu nome completo"
            v-model="user.name"
            class="textInput"
            style="width: 400px"
          />
          <input type="date" v-model="user.dataNasc" class="textInput" />
          <div id="sexVerify">
            <div>
              <input
                type="radio"
                value="masculino"
                v-model="user.sexo"
                class="form-check-input"
              />Masculino
            </div>
            <div>
              <input
                type="radio"
                value="feminino"
                v-model="user.sexo"
                class="form-check-input"
              />Feminino
            </div>
          </div>
          <input
            type="email"
            placeholder="Insira seu email"
            v-model="user.email"
            class="textInput"
            style="width: 1200px"
          />
        </div>
        <div id="secondForm">
          <select
            id="stateSelect"
            v-model="user.estado"
            class="form-select form-select-md textInput"
          >
            <option value="0">Selecione seu estado</option>
            <option v-for="(estado, key) of estados" :value="estado.sigla">
              {{ estado.sigla }}-{{ estado.nome }}
            </option>
          </select>
          <input
            type="text"
            placeholder="Insira sua cidade"
            v-model="user.cidade"
            class="textInput form-control"
          />
          <input
            type="text"
            placeholder="Insira seu endereço"
            v-model="user.endereco"
            class="textInput"
            style="width: 1200px"
          />
        </div>
        <div id="thirdyForm">
          <div>
            <h3>Adicionar Linguagem:</h3>
            <input type="text" placeholder="Nome da linguagem" v-model="lingProg" />
            <button type="button" @click="addLinguage()">Adicionar Linguagem</button>
          </div>
          <div>
            <h3>Principal Linguagem:</h3>
            <select v-model="user.mainLinguage" class="form-select form-select-md textInput">
              <option value="0">Selecione sua principal linguagem</option>
              <option v-for="(linguagem, kay) of user.progLinguages" :value="linguagem">
                {{ linguagem }}
              </option>
            </select>
          </div>
        </div>
        <div id="fourthForm">
          <h3>Seus Hobbies</h3>
          <label for="checkEsporte" class="form-check-label">Esporte</label>
          <input
            name="checkEsporte"
            type="checkbox"
            id="checkEsporte"
            v-model="user.hobbie"
            value="Esporte"
            class="form-check-input"
          />
          <label for="checkLeitura" class="form-check-label">Leitura</label>
          <input
            name="checkLeitura"
            type="checkbox"
            id="checkLeitura"
            v-model="user.hobbie"
            value="Leitura"
            class="form-check-input"
          />
          <label for="checkMusica" class="form-check-label">Musica</label>
          <input
            name="checkMusica"
            type="checkbox"
            id="checkMusica"
            v-model="user.hobbie"
            value="Musica"
            class="form-check-input"
          />
          <label for="checkJogar" class="form-check-label">Jogar</label>
          <input
            name="checkJogar"
            type="checkbox"
            id="checkJogar"
            v-model="user.hobbie"
            value="Jogar"
            class="form-check-input"
          />
          <label for="checkAssistir" class="form-check-label">Assistir</label>
          <input
            name="checkAssistir"
            type="checkbox"
            id="checkAssistir"
            v-model="user.hobbie"
            value="Assistir"
            class="form-check-input"
          />
        </div>
        <button type="submit" id="sendButton">Salvar</button>
      </form>
    </div>
    <div v-else>
      <div id="InfoUser">
        <img :src="user.avatar" style="width: 200px; height: 200px" />
        <p>Nome: {{ user.name }}</p>
        <p>Email: {{ user.email }}</p>
        <p>Data de Nascimento: {{ user.dataNasc.replaceAll('-', '/') }}</p>
        <p>Sex: {{ user.sexo }}</p>
        <p>Endereco: {{ user.endereco }}</p>
        <p>Cidade: {{ user.cidade }}</p>
        <p>Estado: {{ user.estado }}</p>
        <p>Linguagens Conhecidas: {{ user.progLinguages.join(', ') }}</p>
        <p>Principal Linguagem: {{ user.mainLinguage }}</p>
        <p>Hobbies: {{ user.hobbie.join(', ') }}</p>
        <button @click="retornar()">Editar</button>
      </div>
    </div>
  </body>
  <footer></footer>
</template>
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,100;0,200;0,300;0,400;0,500;0,600;0,700;0,800;0,900;1,100;1,200;1,300;1,400;1,500;1,600;1,700;1,800;1,900&display=swap');

* {
  font-family: 'Poppins', sans-serif;
  background-color: transparent;
}

input {
  background-color: white;
}

body {
  background-color: black;
  width: 100vw;
  display: flex;
  justify-content: center;
}

#InfoUser {
  color: white;
}
#InfoUser button {
  appearance: none;
  border: 0px;
  background-color: rgb(110, 110, 250);
  color: white;
  padding: 10px 20px;
}

.validate {
  margin: 50px;
  border-radius: 15px;
  background-color: lightgray;
  display: flex;
  justify-content: center;
  padding: 50px;
  width: 1500px;
}

#firstForm {
  border-radius: 10px;
  width: 1100px;
  gap: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

#secondForm {
  margin: 10px 0px;
  width: 1100px;
  display: flex;
  gap: 20px;
}

#thirdyForm {
  display: flex;
  justify-content: space-around;
  border-radius: 10px;
  padding: 30px 0px 20px 0px;
  background-color: white;
  width: 1100px;
}

#thirdyForm select {
  border: 1px solid lightblue;
}

#thirdyForm input {
  border: 1px solid lightblue;
  padding: 10px;
  border-radius: 10px;
  margin: 10px 15px 0px 0px;
}
#thirdyForm button {
  background-color: rgb(110, 110, 250);
  color: white;
  border: 0px;
  border-radius: 10px;
  padding: 10px;
}
#thirdyForm ul {
  width: 600px;
  display: flex;
  flex-wrap: wrap;
  list-style: none;
  align-items: center;
  font-size: 20px;
}
#thirdyForm ul li {
  margin: 10px;
}
#fourthForm {
  width: 1100px;
  background-color: white;
  border-radius: 10px;
  padding: 20px;
  margin: 20px 0px;
  font-size: 20px;
  display: flex;
  align-items: last baseline;
  justify-content: space-around;
}

.textInput {
  text-align: center;
  appearance: none;
  border: 0px;
  border-radius: 10px;
  height: 50px;
  margin: 10px 0px;
}

#firstForm #sexVerify {
  text-align: left;
  width: 500px;
  font-size: 20px;
  display: flex;
  justify-content: space-around;
  margin: 20px 0px;
}

#avatarUser {
  display: flex;
  justify-content: center;
  height: 200px;
  align-items: baseline;
  margin-bottom: 100px;
}
#avatarUser img {
  border: 1px solid black;
  border-radius: 100%;
  width: 200px;
  height: 200px;
}
#sendButton {
  appearance: none;
  border: 0px;
  background-color: rgb(110, 110, 250);
  font-size: 30px;
  color: white;
  border-radius: 10px;
  padding: 10px 30px;
}
</style>


