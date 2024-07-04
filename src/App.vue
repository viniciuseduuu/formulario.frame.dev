<script setup>
import HelloWorld from './components/HelloWorld.vue'
import TheWelcome from './components/TheWelcome.vue'
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

    <div class="wrapper">
      <HelloWorld msg="You did it!" />
    </div>
  </header>

  <main>
    <TheWelcome />
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
<style scoped>
.altera-titulo 
<div class="container">
  <div class="formulario">
    <h2>Formulário para cadastro do produto</h2>
    <div class="row">
      <label for="">Nome:</label>
      <input type="text" v-model="produto.nome" />
    </div>
    <div class="row">
      <label for="">Preço (em reais):</label>
      <input type="number" step="0.01" v-model="produto.preco" />
    </div>
    <div class="row">
      <label for="">Quantidade:</label>
      <input type="number" v-model="produto.quantidade" />
    </div>

    <fieldset>
      <legend>Unidade de medida</legend>
      <div class="items-radiobox">
        <input type="radio" value="unidade" v-model="produto.medida" /> Unidades
        <input type="radio" value="peso" v-model="produto.medida" /> Peso
      </div>
    </fieldset>
    <fieldset>
      <legend>Categorias</legend>
      <div class="items-checkbox">
        <template v-for="categoria in categorias" :key="categoria.id">
          <input
            type="checkbox"
            :value="categoria.id"
            v-model="produto.categorias"
          />
           {{ categoria.nome }} 
        </template>
      </div>
    </fieldset>
    <button @click="mostrarResultado = !mostrarResultado">Mostrar</button>
  </div>
</div>
{
  background-color: #98e0aa;
  margin: 1rem 2rem;
  border-radius: 20px;
  padding: .75rem;
  display: flex;
  gap: 1rem
}
</style>


