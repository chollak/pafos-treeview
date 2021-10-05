<template>
  <div class="home">
    <button @click="addNew">addNew</button>
    <div class="table-wrapper">
      <table>
        <thead>
          <th>action_type</th>
          <th>url</th>
          <th>number_users</th>
        </thead>
        <tbody>
          <ActionItem
            v-for="item in parentData"
            :node="item"
            :key="item.id"
            @request="sendRequest"
          />
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import ActionItem from "@/components/ActionItem.vue";
import axios from "axios"
/**
 * action url num-user per-user
 */
export default {
  name: "Home",
  components: {
    ActionItem,
  },
  data() {
    return {
      parentData: [
        
      ],
    };
  },
  methods: {
    sendRequest(action) {
      axios
      .get('http://127.0.0.1:5000/get/'+action.id)
      .then(response => (action.children=response.data));
    },
  },
  created(){
    axios
      .get('http://127.0.0.1:5000/get/0')
      .then(response => (this.parentData=response.data));
  }
};

</script>

<style scoped>
.table-wrapper {
  overflow-x: auto;
}
table {
  /* border-collapse: collapse;
  border-spacing: 0; */
  width: 100%;
  border: 1px solid #ddd;
}

th,
td {
  text-align: left;
  padding: 8px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}
</style>