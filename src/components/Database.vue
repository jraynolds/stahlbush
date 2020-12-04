<template>
  <v-card>
    <v-card-title>
      Database
      <v-card-subtitle>{{ descString }}</v-card-subtitle>
      <v-spacer></v-spacer>
      <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Search"
        single-line
        hide-details
      ></v-text-field>
    </v-card-title>

    <v-data-table :headers="data.headers" :items="data.items" :search="search" title="Database">

      <template v-slot:item.buyerAssistance="{ item }">
        <v-icon>
          {{ item.buyerAssistance ? "mdi-check" : "mdi-close" }}  
        </v-icon>
      </template>

      <template v-slot:item.totalCost="{ item }">
        {{ "$" + item.amount * item.cost }}
      </template>
    </v-data-table>
  </v-card>
</template>

<script>
export default {
  props: [ "data", "descString" ],
  data: () => ({
    search: ""
  })
}
</script>

<style>

</style>