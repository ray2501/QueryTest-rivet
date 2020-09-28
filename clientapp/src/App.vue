<template>
    <SqlQuery/>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import SqlQuery from './components/SqlQuery.vue';

export default defineComponent({
  name: 'App',
  components: {
    SqlQuery
  }
});
</script>

