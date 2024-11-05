<template>
  <div>
    <input v-model="searchQuery" placeholder="search" />
    <table>
      <tr>
        <th>Name</th>
        <th>Email</th>
        <th>Status</th>
      </tr>
      <tbody v-if="!searchQuery">
        <tr v-for="(item, idx) in users" :key="idx">
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.status }}</td>
        </tr>
      </tbody>
      <tbody v-else>
        <tr v-for="(item, idx) in filteredUsers" :key="idx">
          <td>{{ item.name }}</td>
          <td>{{ item.email }}</td>
          <td>{{ item.status }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup lang="ts">
import IUser from '~/types/global';
import { users } from '~/data/users';

const searchQuery = ref('');

const filteredUsers = computed(() => {
  return users.filter((user: IUser) => {
    return user.name.toLowerCase().includes(searchQuery.value.toLowerCase()) || user.email.toLowerCase().includes(searchQuery.value.toLowerCase());
  });
});
</script>

<style lang="scss" scoped>
table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  margin-top: 20px;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

tr:nth-child(even) {
  background-color: #dddddd;
}
</style>
