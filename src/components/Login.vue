<template>
<q-layout>
<q-page-container>
    <q-page>
        <div>
        ini page Login
            <div class="flex- flex center">
                <div class="=q-pa-md">
                    <div class="row inline">
                        <q-form
                            @submit="onSubmit"
                            @reset="onReset"
                            class="q-gutter-md"   
                        >
                            <q-input
                                filled
                                v-model="email_address"
                                label="Your Email *"
                                hint="Employee Email"
                                lazy-rules
                                :rules="[ val => val && val.length > 0 || 'Please type something']"
                            />

                            <q-input
                                filled
                                v-model="password"
                                label="Your Password *"
                                hint="Password"
                                lazy-rules
                                :rules="[ val => val && val.length > 0 || 'Please type something']"
                            />
                            <div>
                                    <q-btn label="Submit" type="submit" color="primary"/>
                                    <q-btn label="Reset" type="reset" color="primary" flat class="q-ml-sm" />
                            </div>
                        </q-form>
                    </div>
                </div>    
            </div>     
        </div>
    </q-page>
    </q-page-container>
</q-layout>
</template>



<script>
import Employee from "../api/employee/index";
import { constant } from 'crypto';
import { Script } from 'vm';


export default {
  data() {
    return {
      email_address: "",
      password: "",
      employeeData: []
    };
  },
  methods: {
    onSubmit() {
      let self = this;
      //console.log(self.$router)
      Employee.getLogin(window, self.email_address, self.password)
        .then(function(result) {
          if (!result) {
            self.$q.notify({
              color: "red-5",
              textColor: "white",
              icon: "fas fa-exclamation-triangle",
              message: "You need to accept the license and terms first"
            });
          } else {
            self.$q.notify({
              color: "green-4",
              textColor: "white",
              icon: "fas fa-check-circle",
              message: "Anda Telah Login"
            });
            self.$router.push("register");
          }
          return result;
        })
        .catch(function(err) {
          console.log(err);
        });
    },
    onReset() {
      this.name = null;
      this.age = null;
      this.accept = false;
    }
  }
};
</script>



<style>

</style>
