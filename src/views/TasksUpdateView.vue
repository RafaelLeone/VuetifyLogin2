<template>
  <!-- <v-main class="overflow-hidden mt-4"> -->
  <v-container>
    <v-row>
      <v-col class="pa-1" cols="12">
        <v-card>
          <v-card-text>
            <div>#{{ taskId }}</div>
            <v-form ref="form" @submit.prevent="mudarTarefa(task)">
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
                <v-btn
                  :disabled="!formIsValid"
                  text
                  color="primary"
                  type="submit"
                >
                  Editar tarefa
                </v-btn>
              </v-card-actions>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
  <!-- </v-main> -->
</template>

<script>
import TasksApi from "@/api/tasks.api.js";

export default {
  data: () => {
    return {
      taskId: 0,
      form: {
        first: "",
        last: "",
      },
      rules: {
        name: [(val) => (val || "").length > 0 || "This field is required"],
      },
      snackbar: false,
      deletado: false,
      tarefas: [],
    };
  },
  computed: {
    formIsValid() {
      return this.form.first && this.form.last;
    },
  },
  methods: {
    mudarTarefa(tarefa) {
      const novaTarefa = {
        id: tarefa.id,
        title: this.form.first,
        project: this.form.last,
        status: "pending",
      };
      TasksApi.updateTask(novaTarefa).then(() => {
        this.getTasks();
        this.deletado = true;
      });
      this.$router.go(-1);
    },
    getTasks() {
      TasksApi.getTasks().then((data) => {
        this.tarefas = data;
      });
    },
  },
  created() {
    this.taskId = this.$route.params.id || 0;
    this.task = this.$route.params.task || 0;
    this.getTasks();
  },
};
</script>
