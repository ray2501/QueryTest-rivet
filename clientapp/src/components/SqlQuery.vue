<template>
<div class="query">
<h1 align="center">Query Test</h1>
<div align="center">
<form class="pure-form">
    <fieldset>
    <label for="text">Query String</label>
    <input type="text" class="pure-input-1-2" v-model="sqlstring" placeholder="">
    <button type="submit" class="pure-button pure-button-primary" v-on:click.prevent="posttoserver">Submit</button>
    </fieldset>
</form>
</div>
<table class="pure-table" width="100%">
<thead>
    <tr>
    <td v-for="col in column">{{ col }} </td>
    </tr>
</thead>
<tbody>
    <tr v-for="rowitem in row">
    <td v-for="item in rowitem">{{ item }} </td>
    </tr>
</tbody>
</table>
</div>
</template>

<script lang="ts">
import Vue from 'vue'

var data = {
    sqlstring: '',
    column: '',
    row: ''
}

export default Vue.extend({
  name: 'SqlQuery',
  data () {
    return data
  },
  methods: {
      posttoserver: function () {
         let formdata = new FormData();
         formdata.append('sqlstring', data.sqlstring);
         this.$http.post('sql.rvt', formdata,
         {headers: {'Content-Type': 'application/x-www-form-urlencoded'}})
         .then((response) => {
           data.column = response.data["column"];
           data.row = response.data["row"];
         })
         .catch((error) => {
           alert(error);
         });
     }
  }
})
</script>
