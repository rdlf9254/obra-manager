<template>
  <om-table titulo="Projetos" :dados="dados" :headers="headers"></om-table>
</template>

<script>
import omTable from "@/components/omTable.vue";
export default {
  name: "Home",
  components: {
    omTable,
  },
};
</script>
