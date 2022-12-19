<template>


  <h1>Registration</h1>
  <form action="" @submit.prevent="onSumbit(errors)">
    <div class="field">
      <label for="name">Ім'я</label>
      <input type="text" id="name" name="name" v-model="form.name">
    </div>
    <p>{{ errors.name }}</p>

    <div class="field">

      <label for="surname">Прізвище</label><br>
      <input type="text" id="surname" name="surname" v-model="form.surname">
    </div>
    <p>{{ errors.surname }}</p>

    <div class="field">

      <label for="fatherhood">По-батькові</label><br>
      <input type="text" id="fatherhood" name="fatherhood" v-model="form.fatherhood">
    </div>
    <p>{{ errors.fatherhood }}</p>

    <div class="field">

      <label for="dateOfBirth">Дата Народження</label><br>
      <input type="date" id="dateOfBirth" name="dateOfBirth" v-model="form.dateOfBirth">
    </div>
    <p>{{ errors.dateOfBirth }}</p>

    <div class="field">

      <label for="email">Емайл</label><br>
      <input type="text" id="email" name="email" v-model="form.email">
    </div>
    <p>{{ errors.email }}</p>
    <div class="field">

      <label for="password">Пароль</label><br>
      <input type="password" id="password" name="password" v-model="form.password">
    </div>
    <p>{{ errors.password }}</p>
    <div class="field">

      <label for="phone">Телефон</label><br>
      <input
          name="phone"
          v-model="form.phone"
          v-mask="'38(0##)###-##-##'"
          placeholder="38(0__)___-__-__"
      >
    </div>
    <p>{{ errors.phone }}</p>
    <div class="field" style="flex-direction: row; width: auto; font-size: 20px">

      <input v-model="form.gender" required type="radio" name="gender"
             value="male" id="male-gender">
      <label for="male-gender">Чоловік</label>
      <input v-model="form.gender" type="radio" required name="gender" value="female" id="female-gender">
      <label for="female-gender">Жінка</label>
    </div>
    <div class="field">
      <v-select  style="min-width: 100px" :options="groups" v-model="form.group"></v-select>

    </div>
    <p v-show="!form.group && groupToched">Ви не обрали групу</p>

    <button type="submit">Підтвердити</button>
  </form>
  <Table v-if="table.length" :data="table"></Table>


</template>

<script>
import {defineComponent} from "vue";
import {mask} from 'vue-the-mask'
import Table from './Table.vue'
import vSelect from 'vue-select'
import 'vue-select/dist/vue-select.css'

export default defineComponent({
  name: "Form",
  directives: {
    mask
  },
  components: {Table, vSelect},
  data: () => ({
    errors: {
      name: '',
      surname: '',
      Fatherhood: '',
      dateOfBirth: '',
      email: '',
      password: '',
      gender: '',
      phone: '',
      group: ''
    },
    groups:['ІА-12', 'ІА-13', 'ІА-14', 'ІА-11'],
    groupToched: false,
    form: {
      name: '',
      surname: '',
      fatherhood: '',
      dateOfBirth: '',
      email: '',
      password: '',
      gender: '',
      phone: '',
      group: ''
    },
    table:[

   ]
  }),
  watch: {


    'form.name': {
      handler(val) {
        this.errors.name = this.wordValidation(val, "name");
      }
    },
    'form.surname': {
      handler(val) {

        this.errors.surname = this.wordValidation(val, "surname");
      }
    },
    'form.fatherhood': {

      handler(val) {
        this.errors.fatherhood = this.wordValidation(val, "fatherhood");
      }
    },

    'form.dateOfBirth': {

      handler(val) {
        this.errors.dateOfBirth = this.dateValidation(val);
      }
    },

    'form.email': {

      handler(val) {
        this.errors.email = this.emailValidation(val);
      }
    },

    'form.password': {
      handler(val) {
        this.errors.password = this.passwordValidation(val);
      }
    },

    'form.phone': {
      handler(val) {
        this.errors.phone = this.numValidation(val);
      }
    },

  },

  methods: {
    isFormValid: (errors) => {
      for (let i in errors) {
        if (errors[i]) return false;
      }
      return true;
    },
    onSumbit(errors) {
      if (this.isFormValid(errors)) {
        this.table.push({...this.form, clone: false, delete: false});
        for (let i in this.form){
          this.form[i] = '';
        }

      }
    },

    wordValidation: (value, name) => {
      if (value.length < 3) return name + " should be at least 3 symbols";
      if (value.length > 20) return name + " is too long";
      if (value.match(/[^a-zA-Z-]/)) return name + " contains wrong symbols";
      return "";

    },
    dateValidation: (value) => {
      if (value.length === 0) return "Wrong date:(";
      if ((new Date(value) - new Date()) > 0) return "You are not born yet!";
      return "";
    },
    passwordValidation: (value) => {
      if (value.length < 8) return "Password is too short!";
      return "";
    },
    emailValidation: (value) => {
      if (!value.match(/^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$/) || value.length === 0) return "Email is invalid!";
      return "";
    },
    numValidation: (value) => {
      if (value.length !== 16) return "Please, enter the valid number";
      return "";
    }

  }
});
</script>

<style scoped>
form{
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
p{
  height: 20px;
}
  .field{
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    width: 50%;
  }
  .field>*{
    padding: 0 5px;
  }
  form button{
    margin-top: 10px;
  }
</style>