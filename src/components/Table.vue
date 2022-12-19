<template>
  <table>
    <thead>
    <th>Ім'я</th>
    <th>Прізвище</th>
    <th>По-батькові</th>
    <th>Дата народження</th>
    <th>Емайл</th>
    <th>Парль</th>
    <th>Телефон</th>
    <th>Стать</th>
    <th>Група</th>
    <th>
      <button @click="deleteRows()">Видалити</button>
    </th>
    <th>
      <button @click="cloneRows()">Клонувати</button>
    </th>
    </thead>
    <tbody>
    <tr v-for="(el, i) of data">
      <td>{{ el.name }}</td>
      <td>{{ el.surname }}</td>
      <td>{{ el.fatherhood }}</td>
      <td>{{ el.dateOfBirth }}</td>
      <td>{{ el.email }}</td>
      <td>{{ el.password }}</td>
      <td>{{ el.phone }}</td>
      <td>{{ el.gender }}</td>
      <td>{{ el.group }}</td>
      <td class="buttons">
        <input type="checkbox" v-model="el.delete" :id="i + 'delete'">
        <label :for="i+'delete'">Видалити</label>
      </td>
      <td>
        <input type="checkbox" v-model="el.clone" :id="i + 'copy'">
        <label :for="i+'copy'">Копіювати</label>
      </td>
    </tr>

    </tbody>
  </table>
</template>

<script>
export default {
  name: "Table",
  props: ['data'],
  methods: {
    cloneRows() {
      for (let i of this.data) {
        i.delete = false;
        if (i.clone) {
          i.clone = false;
          this.data.push({...i})
        }
      }
    },
    deleteRows() {
      for (let ind in this.data) {
        if (this.data[ind].delete) {
          this.data.splice(ind, 1);
          this.deleteRows();
        }
      }


    }
  }
}
</script>

<style scoped>
table, tr, th, td {
  border: 1px solid black;
  border-collapse: collapse;
}
</style>