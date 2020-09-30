<template>
<div class="query">
<h1 align="center">Query Test</h1>
<div align="center">
<form class="pure-form">
    <fieldset>
    <label for="text">Query String</label>
    <input type="text" class="pure-input-1-2" v-model="sqlstring" placeholder="">
    <button type="submit" class="pure-button pure-button-primary" @click.prevent="posttoserver">Submit</button>
    </fieldset>
</form>
</div>
<table class="pure-table" width="100%">
<thead>
    <tr>
    <td v-for="col in column" v-bind:key="col">{{ col }} </td>
    </tr>
</thead>
<tbody>
    <tr v-for="rowitem in row" v-bind:key="rowitem">
    <td v-for="item in rowitem" v-bind:key="item">{{ item }} </td>
    </tr>
</tbody>
</table>
</div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import axios from 'axios';

export default defineComponent({
  name: 'SqlQuery',
  data () {
    return {
         sqlstring: '',
         column: '',
         row: ''
      }
  },
  methods: {
      posttoserver(event: string) {
         let formdata = new FormData();
         formdata.append('sqlstring', this.sqlstring);

         axios.post('sql.rvt', formdata,
         {headers: {'Content-Type': 'application/x-www-form-urlencoded'}})
         .then((response) => {
           this.column = response.data["column"];
           this.row = response.data["row"];
         })
         .catch((error) => {
           alert(error);
         });
     }
  }
})
</script>
