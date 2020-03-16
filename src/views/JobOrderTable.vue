<template>
  <v-container text-center>
    <h1>Job Order Report</h1>
    <v-row justify="center">
      <v-card>
          <v-card-title>
             Job Orders
          </v-card-title>
          <v-data-table
            :items="data"
            :headers="headers"
          ></v-data-table>
        </v-card>
    </v-row>
  </v-container>
</template>

<script>
export default {
  mounted(){
    fetch('http://10.1.10.58/aggregatereport/api/statechanges')
    .then(res => res.json())
    .then(data => {
      console.log(data)
      this.data = data
    })
  },
data: ()=>({
  headers: [
      {
        text: "Id",
        align: "left",
        sortable: false,
        value: "id"
      },
      { text: "voltage", value: "voltage" },
      { text: "current", value: "current" },
      { text: "flag", value: "flag" },
      { text: "speed", value: "speed" },
      { text: "rpm", value: "rpm" },
      { text: "sourceId", value: "sourceId" },
      { text: "state", value: "state" },
      { text: "jobOrderId", value: "jobOrderId" },
      { text: "timeStamp", value: "timeStamp" },
      { text: "sequence", value: "sequence" },
    ],
    data:[]
})
}
</script>

<style>

</style>