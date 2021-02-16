<template>
  <div class="home">
    <form>
      <vue-csv-import
          :map-fields="['name', 'number']"
          :headers="['Name', 'Number']"
          v-model="csv"
      >
        <template slot="hasHeaders" slot-scope="{headers, toggle}">
          <label>
            <input :value="headers" @change="toggle" id="hasHeaders" type="checkbox">
            Headers?
          </label>
        </template>

        <template slot="error">
          File type is invalid
        </template>

        <template slot="next" slot-scope="{ load }">
          <div style="margin-top: 1rem;">
            <button
                @click.prevent="load"
                v-if="!csv.length > 0"
            >Load File
            </button
            >
          </div>
        </template>

        <template slot="submit">
          <button @submit.prevent="onSubmitCsv">Submit!</button>
        </template>
      </vue-csv-import>

    </form>

  </div>
</template>

<script>
    import {VueCsvImport} from 'vue-csv-import'

    export default {
        components: {VueCsvImport},

        data() {
            return {
                csv: [],
            }
        },

        methods: {
            onSubmitCsv() {
                try {
                    if (this.csv.length > 0) {
                        console.info(this.csv)
                    } else {
                        return new Error('There are no entries in the file!')
                    }

                } catch (error) {
                    console.error(error.message)
                }
            },
        },
    }
</script>
