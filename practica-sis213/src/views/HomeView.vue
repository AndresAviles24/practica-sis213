<template>
  <div>
    <h2>Lista de paises</h2>

    <form @submit.prevent="saveTask()">
        
        <div class="form-group">
          <label for="label">Etiqueta</label>
          <div class="input-group">
            <select class="form-control" id="label" v-model="form.labelId">
              <option
                v-for="country in countries"
                :value="country.countryId"
                :key="country.countryId"
              >
                {{ country.countryName }}
              </option>
            </select>
          </div>
        </div>

        <br />
        <div class="text-center">
          <button id="submit-button" type="submit" class="btn btn-primary" style="background-color: hsl(120, 73%, 39%);">
            Guardar
          </button>
        </div>
      </form>


  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "homeView",
  data: function(){
    return {
      form: {
        countryId: "",
        stateId: "",
        cityId: "",
      },
      // Para listado
      countries: [],
      states: [],
      cities: [],
    };
  },
  mounted: function() {
      //Llenado de las etiquetas
      axios
        .get("http://localhost:8080/api/v1/country")
        .then((response) => {
          this.countries = response.data.result;
        });
  }
}

</script>
