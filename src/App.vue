<template>
  <div class="wrapper">
      <Form></Form>
  </div>
</template>

<style scoped>
.wrapper{
  display: flex;
  flex-direction: column;
  align-items: center;
  width:100%;
}

</style>
<script>
import {defineComponent} from 'vue'

import vSelect from "vue-select";
import 'vue-select/dist/vue-select.css'
import {mask} from 'vue-the-mask'
import Form from './components/Form.vue'
export default defineComponent({
  name:"app",
  props: {
    //Реквізити - https://ua.vuejs.org/guide/components/props.html#props-declaration
  },
  components: {
    Form,
    //Локальна реєстрація компонентів
    // https://ua.vuejs.org/guide/components/registration.html#local-registration
    vSelect,

  },
  directives: {
    //Локальна реєстрація директив
    mask
  },
  data: () => ({

  }),
  watch: {
    //Спостерігачі
    variableName: function (variableVale) {
      //більш детально https://ua.vuejs.org/guide/essentials/watchers.html#base-example
    }
  },

});
</script>