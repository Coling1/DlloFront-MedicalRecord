<template>
  <v-row justify="center" align="center">
    <v-col cols="12">
      <v-card flat>
        <v-card-actions>
          <h1>Listado de historias</h1>
          <v-spacer></v-spacer>
          <v-btn color="success" class="text-none" to="/historias/creacion"
            >Crear historia</v-btn
          >
        </v-card-actions>
        <v-card-text>
          <v-data-table
            :headers="headers"
            :items="historias"
            :items-per-page="5"
            class="elevation-1"
          >
            <template v-slot:[`item.actions`]="{ item }">
              <v-icon class="mr-2" @click="editItem(item)">
                mdi-pencil
              </v-icon>
              <v-icon @click="deleteItem(item)">
                mdi-delete
              </v-icon>
            </template>
          </v-data-table>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  beforeMount() {
    this.getHistorias();
  },
  data() {
    return {
      headers: [
        {
          text: "Nombre",
          align: "start",
          value: "name",
        },  
            
        { text: "Apellidos", value: "apellidos" },
        { text: "Identificación", value: "id" },     
        { text: "Fecha", value: "fecha" },   
        { text: "Hora", value: "hora" },        
        { text: "EPS", value: "eps" },
        { text: "Estado Civíl", value: "estadoCivil" },
        { text: "Médico Tratante", value: "medicoTratante" },
        { text: "Observaciones", value: "observaciones" },
        { text: "Acción", value: "actions" },
      ],
      historias: [],
    };
  },
  methods: {
    /**
     * Enviar una solicitud (Request) en un método get
     * Para consultar todos las historias
     */
    async getHistorias() {
      try {
        let response = await this.$axios.get("http://localhost:3001/historias");
        this.historias = response.data;
      } catch (error) {
        console.error(error);
      }
    },
    /**
     * Enviar el producción a edición
     * /historias/id
     */
    editItem(item) {
      let url = `/historias/${item.id}`;
      this.$router.push(url);
    },
    /**
     * Eliminar una historia
     */
    deleteItem(item) {
      this.$swal
        .fire({
          type: "warning",
          title: "¿Está seguro de eliminar el item?",
          text: "Al borrar el item no se podrá recuperar.",
          allowEscapeKey: false,
          allowOutsideClick: false,
          showCancelButton: true,
        })
        .then(async (result) => {
          if (result.value) {
            try {
              let url = "http://localhost:3001/historias/" + item.id;
              await this.$axios.delete(url);
              this.$swal.fire({
                type: "success",
                title: "Operación exitosa.",
                text: "El item se eliminó correctamente.",
              });
              this.getHistorias();
            } catch (error) {
              this.$swal.fire({
                type: "error",
                title: "Ha ocurrido un problema al eliminar",
                text: error.toString(),
              });
            }
          }
        });
    },
  },
};
</script>
