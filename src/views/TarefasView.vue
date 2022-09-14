<template>
  <div>
    <v-list flat subheader three-line>
      <v-subheader>General</v-subheader>

      <v-list-item-group multiple active-class="">
        <div v-for="(tarefa, index) in tarefas" :key="index">
          <TarefaView :tarefa="tarefa" @salvarClick="recebiSalvar(index)" />
        </div>
      </v-list-item-group>
    </v-list>
  </div>
</template>

<script>
import TarefaView from "../components/tarefas/TarefaView.vue";

export default {
  name: "HomeView",

  components: {
    TarefaView,
  },
  data() {
    return {
      tarefas: [
        { titulo: "Ir ao mercado", concluido: false },
        { titulo: "Comprar ração", concluido: false },
      ],
    };
  },
  methods: {
    recebiSalvar(index) {
      console.log("entrei");
      this.tarefas[index].concluido = !this.tarefas[index].concluido;
    },
  },
};
</script>
