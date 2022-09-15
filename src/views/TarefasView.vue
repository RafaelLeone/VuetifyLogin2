<template>
  <div>
    <v-list flat subheader three-line>
      <v-card flat>
        <v-snackbar v-model="snackbar" absolute bottom right color="success">
          <span>Registration successful!</span>
          <v-icon dark> mdi-checkbox-marked-circle </v-icon>
        </v-snackbar>
        <v-form ref="form" @submit.prevent="submit">
          <v-container fluid>
            <v-row>
              <v-col cols="12" sm="6">
                <v-text-field
                  v-model="form.first"
                  :rules="rules.name"
                  color="purple darken-2"
                  label="Nome da nova tarefa"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6">
                <v-text-field
                  v-model="form.last"
                  :rules="rules.name"
                  color="blue darken-2"
                  label="Descrição da tarefa"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <v-card-actions>
            <v-btn :disabled="!formIsValid" text color="primary" type="submit">
              Registrar nova tarefa
            </v-btn>
          </v-card-actions>
        </v-form>
      </v-card>
      <v-col cols="12"> </v-col>
      <v-subheader>Tarefas:</v-subheader>

      <v-list-item-group multiple active-class="">
        <div v-for="(tarefa, index) in tarefas" :key="index">
          <TarefaView :tarefa="tarefa" @salvarClick="recebiSalvar(index)" />
        </div>
      </v-list-item-group>
    </v-list>
  </div>
</template>

<script>
import TasksApi from "../TasksApi.js";
import TarefaView from "../components/tarefas/TarefaView.vue";

export default {
  name: "HomeView",

  components: {
    TarefaView,
  },
  data() {
    const defaultForm = Object.freeze({
      first: "",
      last: "",
    });
    return {
      form: Object.assign({}, defaultForm),
      rules: {
        name: [(val) => (val || "").length > 0 || "This field is required"],
      },
      snackbar: false,
      defaultForm,
      tarefas: [
        // {
        //   titulo: "Ir ao mercado",
        //   descricao: "Comprar pão, café e iogurte",
        //   concluido: false,
        // },
        // {
        //   titulo: "Comprar ração",
        //   descricao: "A última foi a verde dos dois",
        //   concluido: false,
        // },
      ],
    };
  },
  computed: {
    formIsValid() {
      return this.form.first && this.form.last;
    },
  },

  methods: {
    resetForm() {
      this.form = Object.assign({}, this.defaultForm);
      this.$refs.form.reset();
    },
    submit() {
      this.snackbar = true;
      this.resetForm();
      const novaTarefa = {
        titulo: this.form.first,
        descricao: this.form.last,
        concluido: false,
      };
      this.tarefas.push(novaTarefa);
    },
    recebiSalvar(index) {
      console.log("entrei");
      this.tarefas[index].concluido = !this.tarefas[index].concluido;
    },
    listarTarefas() {
      TasksApi.getTasks((data) => {
        this.tarefas = data;
      });
    },
  },
  created() {
    this.listarTarefas();
  },
};
</script>
