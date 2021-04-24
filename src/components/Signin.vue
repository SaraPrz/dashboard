<template>
  <v-container>
    <v-row class="text-center">
      <v-col
        class="d-flex"
        cols="20"
      >
        <v-form
        ref="form"
        lazy-validation
        cols="20"
        >
          <v-select
            :items="items"
            label="Standard"
            v-model="selectedUser"
            @click="selectUser"
          ></v-select>
          <v-btn
          color="success"
          @click="submit"
          class="login float-right"
          >
          ورود
          </v-btn>
          <v-btn
          color="error"
          @click="clear"
          class="reset float-left"
          >
          پاک کردن
          </v-btn>
        </v-form>
      </v-col>
    </v-row>
    <div v-if="role==='admin'">
      <Admin></Admin>
    </div>
    <div v-if="role==='user'">
      <User></User>
    </div>
  </v-container>
</template>
  
<script>
import Admin from "./Admin"
import User from "./User"
  export default {
    name: 'Signin',
    components: {
      Admin,
      User
    },
    data: () => ({
      items: ['admin','user'],
      selectedUser: '',
      role: ''
    }),
    methods: {
      clear() {
        this.$refs.form.reset();
        localStorage.removeItem('auth');
      },
      submit() {
        localStorage.setItem("auth" ,this.selectedUser);
        this.role = localStorage.getItem("auth");
      }
    }
  }
</script>
<style>
  form {
    width: 100%;
  }

</style>
