<template>
  <v-container>
    <v-row class="text-center">
      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">Formulario de ALTA</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <form v-on:submit.prevent="guardarArticulo()">
          <v-text-field
            v-model="articulo.descripcion"
            label="Descripción"
            outlined
            required
          >
          </v-text-field>
          <v-text-field
            v-model="articulo.precio"
            label="Precio"
            type="number"
            prefix="$"
            outlined
            required
          ></v-text-field>
          <v-text-field
            v-model="articulo.stock"
            label="Stock"
            type="number"
            outlined
            required
          ></v-text-field>
          <v-card-actions>
            <v-btn color="warning" class="mr-4" type="submit">Guardar</v-btn>
          </v-card-actions>
        </form>
      </v-col>
    </v-row>
  </v-container>
</template>
<script>
import axios from "axios";
export default {
  name: "crearArticulo",
  data() {
    return {
      articulo: {
        descripcion: "",
        precio: "",
        stock: "",
      },
    };
  },
  methods: {
    async guardarArticulo() {
      try {
        const router = this.$router;

        const data = {
          descripcion: this.articulo.descripcion,
          precio: this.articulo.precio,
          stock: this.articulo.stock,
        };

        const response = await axios.post(
          "http://localhost:8050/api/articulos",
          data
        );

        if (response.status == 201) {
          router.push("/articulos");
        }
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>
