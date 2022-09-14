<template>
  <div>
    <v-list flat subheader three-line>
      <v-subheader>General</v-subheader>

      <v-list-item-group v-model="settings" multiple active-class="">
        <TarefaView />
        <TarefaView />
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
};
</script>
