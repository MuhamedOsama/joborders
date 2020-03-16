<template>
  <div class="text-center">
    <v-dialog v-model="dialog" width="500">
      <template v-slot:activator="{ on }">
        <v-btn dark v-on="on">
          Edit
        </v-btn>
      </template>
      <v-card>
        <v-card-title class="headline grey lighten-2" primary-title>
         Edit
        </v-card-title>
        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-text-field
              v-model="title"
              :counter="10"
              :rules="nameRules"
              label="Title"
              required
            ></v-text-field>
            <v-text-field
              v-model="content"
              label="Content"
              required
            ></v-text-field>
            <v-text-field
              v-model="person"
              :rules="nameRules"
              label="Author"
              required
            ></v-text-field>
            <v-col class="d-flex" cols="12" sm="6">
              <v-select
                v-model="status"
                :items="items"
                label="Outlined style"
                outlined
              ></v-select>
            </v-col>
            <v-btn class="mr-4" @click="validate" :loading="loading"
              >submit</v-btn
            >
            <v-btn @click="reset">clear</v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
export default {
  name: "Edit",
  data: () => ({
  })
};
</script>