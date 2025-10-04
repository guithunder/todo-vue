<template>
  <div id="app">
    <h1>Lista de Tarefas Simples</h1>

    <div class="bloco-adicionar-tarefa">
      <input 
        type="text"
        v-model="textoNovaTarefa"
        placeholder="Adicione uma nova tarefa..."
        @keyup.enter="adicionarTarefa"
      >
      <button @click="adicionarTarefa">Adicionar</button>
    </div>

    <ul class="lista-de-tarefas">
      <li 
        v-for="tarefa in tarefas" 
        :key="tarefa.id"
        :class="['item-tarefa', { 'tarefa-concluida': tarefa.concluida }]"
      >
        <span @click="toggleConcluida(tarefa.id)">{{ tarefa.texto }}</span>
        
        <button @click="removerTarefa(tarefa.id)">Remover</button>
      </li>
    </ul>

    <p v-if="tarefas.length === 0" class="sem-tarefas">
      Nenhuma tarefa pendente parabéns! 🔥
    </p>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// ESTADO DE AD
const tarefas = ref([]); 
const textoNovaTarefa = ref(''); 

//  TODAS FUNÇÕES 
const adicionarTarefa = () => {
  if (textoNovaTarefa.value.trim() === '') return;

  const novaTarefa = {
    id: Date.now(), 
    texto: textoNovaTarefa.value.trim(), 
    concluida: false 
  };

  tarefas.value.push(novaTarefa);
  textoNovaTarefa.value = ''; 
};

const removerTarefa = (idTarefa) => {
  tarefas.value = tarefas.value.filter(t => t.id !== idTarefa);
};

const toggleConcluida = (idTarefa) => {
  const tarefa = tarefas.value.find(t => t.id === idTarefa);
  if (tarefa) {
    tarefa.concluida = !tarefa.concluida;
  }
};
</script>

<style scoped>

#app {
  max-width: 500px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #053ffc; 
  border-radius: 4px;
  font-family: sans-serif;
}

h1 {
  text-align: center;
  margin-bottom: 25px;
  color: #10f023;
}

/* box de adição */
.bloco-adicionar-tarefa {
  display: flex;
  margin-bottom: 20px;
  gap: 8px;
}


/*botao de ad atv o verde*/ 
.bloco-adicionar-tarefa input {
  flex-grow: 1;
  padding: 8px;
  border: 1px solid #0aee69;
  border-radius: 3px;
}

.bloco-adicionar-tarefa button {
  
  background-color: #00ff80; 
  color: #333;
  border: 1px solid #0de77a;
  padding: 8px 12px;
  border-radius: 3px;
  cursor: pointer;
}


.lista-de-tarefas {
  list-style: none;
  padding: 0;
}




/* Tarefas por vez */
.item-tarefa {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  margin-bottom: 6px;
  background-color: rgb(38, 38, 49); 
  border: 1px solid #131518; 
  border-radius: 3px;
}

.item-tarefa span {
  flex-grow: 1;
  cursor: pointer;
}




/* Estilo para Tarefa Concluída */
.tarefa-concluida {
  background-color: #02ff2c; 
  border-color: #2bff00;
}


 /* Riscador do texto da atv feita */
.tarefa-concluida span {
  text-decoration: line-through; 
  color: #000000;
}


/* botao de remove da lista o red ai ai */
.item-tarefa button {
  
  background-color: red;
  color: #0e0d0d;  
  border: 1px solid #cc0000;
  padding: 4px 8px;
  margin-left: 10px;
  border-radius: 3px;
  cursor: pointer;
}

/* box sem atv estilo*/ 
.sem-tarefas {
  text-align: center;
  color: #888;
  margin-top: 30px;
  font-style: italic;
}
</style>