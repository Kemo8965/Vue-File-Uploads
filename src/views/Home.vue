<script>
import { VueCsvImport } from 'vue-csv-import'

export default {
  components: { VueCsvImport },

  data() {
    return {
      csv: {
        name: '',
        number: '',
      },
    }
  },

  methods: {
    onSubmitCsv() {
      try {
        if (this.csv.length > 0) {
          console.info(this.csv)
        } else {
          throw new Error('There are no entries in the file!')
        }

      } catch (error) {
        console.error(error.message)
      }
    },
  },
}
</script>

<template>
<div class="home">
          <form @submit.prevent="onSubmitCsv">
            <vue-csv-import
              v-model="csv"
              :map-fields="{name: 'Name', number: 'Number'}"
            >
              <template slot="hasHeaders" slot-scope="{headers, toggle}">
        <label>
            <input type="checkbox" id="hasHeaders" :value="headers" @change="toggle">
            Headers?
        </label>
    </template>

    <template slot="error">
        File type is invalid
     </template>
    
              <template slot="next" slot-scope="{ load }">
                <div>
                  <button
                    v-if="!csv.length > 0"
                    @click.prevent="load"
                    >Load File</button
                  >
                </div>
              </template>
            </vue-csv-import>
            
          </form>

          </div>
</template>
