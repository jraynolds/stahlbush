<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >

      <v-spacer/>
        Stahlbush App
      <v-spacer/>
    
    </v-app-bar>

    <v-main>

      <v-container>
        <v-row>
          <v-card-subtitle class="pt-6">You are Richard Thomas, a</v-card-subtitle>
          <v-select class="flex-grow-0" v-model="role" :items="roles" />
          <v-card-subtitle class="pt-6">in</v-card-subtitle>
          <v-select class="flex-grow-0" v-model="department" :items="departments" />
        </v-row>

        <Database :data="selectDataTables" :descString="filterText.worker" />

      </v-container>

    </v-main>
  </v-app>
</template>

<script>
export default {
  name: 'App',

  components: {
    Database: () => import("@/components/Database.vue")
  },

  data: () => ({
    role: "Worker",
    roles: [ "Worker", "Manager", "Admin" ],
    department: "Landscaping",
    departments: [ "Landscaping", "Home Improvement", "R&D" ],

    filterText: {
      worker: "where the only items are in your department"
    },

    data: {
      headers: [
        { text: 'Requisition number', align: 'start', value: 'number', width: 100 },
        { text: 'Status', value: 'status' },
        { text: 'Buyer assistance?', value: 'buyerAssistance', width: 50 },
        { text: 'Item', value: 'item' },
        { text: 'Notes', value: 'notes' },
        { text: 'Date', value: 'date' },
        { text: 'Department', value: 'dept' },
        { text: 'Requester', value: 'requester' },
        { text: 'Buyer', value: 'buyer' },
        { text: 'Shipping Method', value: 'shipMethod' },
        // { text: 'Amount', value: 'amount' },
        // { text: 'Item cost', value: 'cost' },
        { text: 'Total cost', value: "totalCost" },
      ],
      items: [
        {
          number: 1,
          status: "REQUESTED",
          buyerAssistance: false,
          item: "Bag of dirt",
          notes: "This is a bag of dirt.",
          date: "11/29/2020",
          dept: "Landscaping",
          requester: "Richard T.",
          buyer: "Home Depot",
          shipMethod: "Standard Ground",
          amount: 8,
          cost: 50
        },
        {
          number: 2,
          status: "APPROVED",
          buyerAssistance: true,
          item: "Small shrubs",
          notes: "Bougenvalia.",
          date: "11/26/2020",
          dept: "Landscaping",
          requester: "Jasper R.",
          buyer: "Lowe's",
          shipMethod: "Air Mail",
          amount: 16,
          cost: 10
        },
        {
          number: 3,
          status: "REQUESTED",
          buyerAssistance: false,
          item: "Box of nails",
          notes: "4mm.",
          date: "11/28/2020",
          dept: "Home Improvement",
          requester: "James C.",
          buyer: "Home Depot",
          shipMethod: "Expedited",
          amount: 100,
          cost: .05
        },
      ]
    }
  }),
  computed: {
    selectDataTables() {
      let department = this.department;
      return {
        headers: this.data.headers,
        items: this.data.items.filter(item => item.dept === department)
      }
    }
  }
};
</script>
