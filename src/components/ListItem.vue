<template>
  <div>
    <h1>List Item</h1>
    <table class="table table-striped">
      <thead>
        <tr>
          <th>Item Name</th>
          <th>Item Price</th>
          <th colspan="2">Action</th>
        </tr>
      </thead>
      <tbody>
          <tr v-for="item of items" :key="item['.key']">
            <td>{{ item.name }}</td>
            <td>{{ item.price }}</td>
            <td>
                <router-link :to="{ name: 'Edit', params: {id: item['.key']} }" class="btn btn-warning">
                  Edit
                </router-link>
            </td>
            <td>
              <button @click="deleteItem(item['.key'])" class="btn btn-danger">Delete</button>
            </td>
          </tr>
      </tbody>
    </table>
  </div>
</template>

<script>

import { db } from '../config/db';

export default {
  components: {
      name: 'ListItem'
  },
  data() {
    return {
      items: []
    }
  },
  firebase: {
    items: db.ref('items')
  },
  methods: {
    deleteItem(key) {
      this.$firebaseRefs.items.child(key).remove();
    }
  }
}
</script>