<template>
  <div class="dash" v-if="show">
    <h1 class="text-center white--text">Job Order</h1>
    <v-container class>
      <v-row justify="center" v-if="state == 1">
        <v-col cols="12" sm="6" md="6" lg="6">
          <v-card class="mx-auto card" min-width="600px">
            <v-card-text
              class="subheading font-weight-bold headline text-center"
            >{{ item.sourceId }} (Job Order)</v-card-text>
            <v-divider></v-divider>
            <v-list dense>
              <v-list-item>
                <v-list-item-content>Voltage:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.voltage }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>Current:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.current }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>state:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.state }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>Speed:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.speed }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>RPM:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.rpm }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>Flag:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.flag }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>jobOrderId:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.jobOrderId }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>timeStamp:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.timeStamp }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>sequence:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.sequence }}</v-list-item-content>
              </v-list-item>
            </v-list>
            <v-card-actions>
              <v-btn justify="center" @click="Edit">Edit</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <v-row justify="center" v-if="state == 2" >
        <v-col cols="12" sm="6" md="6" lg="6">
          <v-card class="mx-auto card"  min-width="600px">
            <v-card-text
              class="subheading font-weight-bold headline text-center"
            >{{ item.sourceId }} Error (stoppage)</v-card-text>
            <v-divider></v-divider>
            <v-list dense>
              <v-list-item>
                <v-list-item-content>Voltage:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.voltage }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>Current:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.current }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>state:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.state }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>Speed:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.speed }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>RPM:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.rpm }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>Flag:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.flag }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>jobOrderId:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.jobOrderId }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>timeStamp:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.timeStamp }}</v-list-item-content>
              </v-list-item>
              <v-list-item>
                <v-list-item-content>sequence:</v-list-item-content>
                <v-list-item-content class="align-end">{{ item.sequence }}</v-list-item-content>
              </v-list-item>
            </v-list>
            <v-card-actions>
              <v-btn justify="center" @click="EditError">Edit</v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
      <div class="text-center">
        <v-dialog v-model="dialog" width="500">
          <v-card>
            <v-card-title class="headline grey lighten-2" primary-title>Edit Job Order</v-card-title>

            <v-card-actions>
              <v-combobox :value="reportJobOrder" v-model="reportJobOrder" :items="joborders"></v-combobox>
            </v-card-actions>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="SendEdit">I accept</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
       <div class="text-center">
        <v-dialog v-model="dialog2" width="500">
          <v-card>
            <v-card-title class="headline grey lighten-2" primary-title>Edit Error</v-card-title>

            <v-card-actions>
              <v-combobox :value="reportError" v-model="reportError" :items="Errors"></v-combobox>
            </v-card-actions>

            <v-divider></v-divider>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="primary" text @click="SendEditError">I accept</v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      </div>
    </v-container>
  </div>
</template>
<script>
// @ is an alias to /src
export default {
  name: "Home",
  
  mounted() {
        this.fetchData()
    setInterval(() => this.fetchData(), 5000);
  },
  data: () => ({
    show: true,
    cards: [],
    item:null,
    timer:null,
    voltage: 0.0,
    joborders:null,
    reportJobOrder:null,
    current: 0.0,
    flag: 0,
    speed: 0,
    dialog:false,
    dialog2:false,
    rpm: 0,
    reportError:null,
    Errors:[],
    state: 0,
    jobOrderId: null,
    timeStamp: null
  }),
  methods: {
    Edit(){
      this.dialog = true
      fetch(`http://10.1.10.58/aggregatereport/api/joborders/${this.report.sourceId}`)
      .then(res => res.json())
      .then(data => {
        this.joborders = data.map(el => ({
          text:el.jobOrderId,
          value:el.jobOrderId
        }))
        console.log(data)
      })
    },
    async SendEdit(){
      this.report.jobOrderId = this.reportJobOrder.value
      console.log(this.report)
    const response = await fetch(`http://10.1.10.58/aggregatereport/api/statechanges/${this.report.id}`,{
              method: 'PUT',
                        headers: {
                            'Access-Control-Allow-Origin':'*',
                            'Accept': 'application/json',
                            'Content-Type': 'application/json',
                            
                        },
                        body: JSON.stringify(this.report)
          })
          console.log(await response)
          
          this.dialog = false
  //console.log(content);
},
    EditError(){
      this.dialog2 = true
      fetch(`http://10.1.10.58/aggregatereport/api/errorcodes`)
      .then(res => res.json())
      .then(data => {
        this.Errors = data.map(el => ({
          text:` (${el.stoppageSequence}) ${el.translation}` ,
          value:el.stoppageSequence
        }))
        console.log(data)
      })

    },
    
async SendEditError(){
  this.report.sequence = this.reportError.value.toString()
      console.log(this.report)
    const response = await fetch(`http://10.1.10.58/aggregatereport/api/statechanges/${this.report.id}`,{
              method: 'PUT',
                        headers: {
                            'Access-Control-Allow-Origin':'*',
                            'Accept': 'application/json',
                            'Content-Type': 'application/json',
                            
                        },
                        body: JSON.stringify(this.report)
          })
          console.log(await response)
          
          this.dialog2 = false
  //console.log(content);
  console.log(this.report)

},
fetchData(){
  console.log("fetching")
  fetch("http://10.1.10.58/aggregatereport/api/statechanges/51")
      .then(response => {
        return response.json();
      })
      .then(data => {
        console.log(data)
        this.report = data;
        this.item = {
          sourceId: this.report.sourceId,
          voltage: this.report.voltage,
          current: this.report.current,
          flag: this.report.flag,
          speed: this.report.speed,
          rpm: this.report.rpm,
          state: this.report.state,
          sequence: this.report.sequence,
          jobOrderId: this.report.jobOrderId,
          timeStamp: new Date(this.report.timeStamp).toDateString()
        }
        this.reportJobOrder = this.report.jobOrderId
        this.state = this.report.state
      });
}
    },
    sortBy(prop) {
      this.projects.sort((a, b) => (a[prop] < b[prop] ? -1 : 1));
    }
  }

</script>
<style></style>