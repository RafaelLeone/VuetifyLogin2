<template>
  <div>
    <v-list flat subheader three-line>
      <v-subheader>General</v-subheader>

      <v-list-item-group v-model="settings" multiple active-class="">
        <div v-for="(tarefa, index) in tarefas" :key="index">
          <TarefaView :tarefa="tarefa" />
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
};
</script>
