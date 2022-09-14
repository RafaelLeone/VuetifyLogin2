<template>
  <div>
    <v-list-item :class="tarefa.concluido ? 'blue' : 'red'">
      <template v-slot:default="{}">
        <v-list-item-action>
          <v-checkbox
            @click="salvarClique"
            :input-value="tarefa.concluido"
          ></v-checkbox>
        </v-list-item-action>

        <v-list-item-content>
          <v-list-item-title>{{ tarefa.titulo }}</v-list-item-title>
          <v-list-item-subtitle
            >Notify me about updates to apps or games that I
            downloaded</v-list-item-subtitle
          >
        </v-list-item-content>
      </template>
    </v-list-item>
  </div>
</template>

<script>
export default {
  props: ["tarefa"],
  methods: {
    salvarClique() {
      this.$emit("salvarClick");
    },
  },
};
</script>
