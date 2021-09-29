<template>
  <div class="home">
    <button @click="addNew">addNew</button>
    <div class="table-wrapper">
      <table>
        <thead>
          <th>url</th>
          <th>percent_stopped</th>
          <th>action_type</th>
          <th>number_users</th>
          <th>stopped</th>
          <th>LEVEL</th>
        </thead>
        <tbody>
          <ActionItem
            v-for="item in mergedData"
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
        {
          action_type: "load site",
          id: 1,
          number_users: 433,
          parent_id: 0,
          percent_stopped: 69.0531,
          percent_users: 2.70777,
          stopped: 299,
          url: "https://axmap.ae/",
          children: [
            {
              action_type: "SHUKUR",
              id: 22,
              number_users: 433,
              parent_id: 1,
              percent_stopped: 69.0531,
              percent_users: 2.70777,
              stopped: 299,
              url: "https://axmap.ae/child",
            },
          ],
        },
        {
          action_type: "GG site",
          id: 2,
          number_users: 433,
          parent_id: 0,
          percent_stopped: 69.0531,
          percent_users: 2.70777,
          stopped: 299,
          url: "https://axmap.ae/",
        },
        {
          action_type: "load site",
          id: 3,
          number_users: 433,
          parent_id: 0,
          percent_stopped: 69.0531,
          percent_users: 2.70777,
          stopped: 299,
          url: "https://axmap.ae/",
        },
      ],
    };
  },
  computed: {
    mergedData() {
      return [...this.parentData];
    },
  },
  methods: {
    sendRequest(action) {
      console.log(action);
      const result = [
        {
          action_type: "load site",
          id: 322,
          number_users: 433,
          parent_id: 22,
          percent_stopped: 69.0531,
          percent_users: 2.70777,
          stopped: 299,
          url: "https://axmap.ae/child",
        },
      ];
      // const index = this.parentData.findIndex((item) => item.id === id);
      action.children = result;
    },
    addNew() {
      setTimeout(() => {
        this.thirdData = [
          {
            action_type: "load site",
            id: 2,
            number_users: 53,
            parent_id: 2,
            percent_stopped: 9.43396,
            percent_users: 12.2402,
            stopped: 5,
            url: "https://axmap.ae/uae/properties-for-sale",
          },
          {
            action_type: "input search",
            id: 6844,
            number_users: 37,
            parent_id: 2,
            percent_stopped: 0.0,
            percent_users: 8.54503,
            stopped: 0,
            url: "https://axmap.ae/",
          },
        ];
      }, 3500);
    },
  },
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