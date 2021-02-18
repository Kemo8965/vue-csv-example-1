<template>
  <div class="container" id="app">
    <div class="row">
      <div class="two columns"></div>
      <div class="eight columns">

        <div style="text-align:center; padding-top:30px;"><h3>Fleet Upload</h3></div>
        <div class="banner">
           

        <h5>Example Template</h5>
         <p>You can download <a href="../public/example.csv">this template</a> for your convenience.</p>
        </div>
       
       
        <form @submit.prevent="onSubmit">
          <!--          :map-fields="['name', 'age']"-->
          <vue-csv-import
    
              :headers="['Name', 'Age']"
              :map-fields="{id_number: 'ID', vehicle_make: 'Vehicle Make', vehicle_model: 'Vehicle Model', year_of_make: 'Year Of Make', chasis_number:'Chasis Number'}"
              :can-ignore="false"
              :file-mime-types="['text/csv']"
              auto-match-fields
              auto-match-ignore-case
              table-class="u-full-width"
              v-model="csv"
          >

            <template slot="next" slot-scope="{ load }">
              <div class="d-flex justify-content-end">
                <button style="background-color:beige; outline:none; color:black; border-radius: 0 15px 0 15px"
                    @click.prevent="load"
                    v-if="!csv.length > 0"
                >Load File
                </button
                >
              </div>
            </template>
          </vue-csv-import>
          <table class="u-full-width" style="background-color:beige; border-radius:5px; outline:none; color:black; border: 1px solid black;">
            <thead>
            <tr>
              <th>ID</th>
              <th>Vehicle Make</th>
              <th>Vehicle Model</th>
              <th>Year Of Make</th>
              <th>Chasis Number</th>
            </tr>
            </thead>
            <tbody>
            <tr :key="index" v-for="(person, index) in csv">
              <td>{{ person.id_number }}</td>
              <td>{{ person.vehicle_make }}</td>
              <td>{{ person.vehicle_model }}</td>
              <td>{{ person.year_of_make }}</td>
              <td>{{ person.chasis_number }}</td>
            </tr>
            </tbody>
          </table>

          <button type="submit">Submit CSV</button>
        </form>

        <pre><code>{{ csv }}</code></pre>
      </div>
    </div>
  </div>
</template>

<script>
    import {VueCsvImport} from 'vue-csv-import'

    export default {
        name: 'App',
        components: {
            VueCsvImport
        },

        data: () => ({
            csv: []
        }),

        methods: {
            onSubmit() {
                alert(`Data entered: ${JSON.stringify(this.csv)}`)
            }
        }
    }
</script>

<style scoped>
.banner {
  background-color: beige;
  width: auto;
  color: black;
  border: 1px solid black;
  text-align: center;
}
</style>