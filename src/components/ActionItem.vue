<template>
  <tr>
    <td :style="nodeMargin">
      <button @click="sendRequest(node, hasChildren)">
        {{ hasChildren ? showChildren ? "-" : "+" : '+' }}
      </button>
      {{ node.action_type }}
    </td>
    <td style="max-width: 500px">{{ node.url }}</td>
    <td>{{ node.number_users }} [{{node.percent_users.toFixed(2)}}%]</td>
  </tr>
  <tr v-if="hasChildren" v-show="showChildren">
    <ActionItem
      
      v-for="child in node.children"
      :spacing="spacing + 10"
      :key="child.id"
      :node="child"
      @request="sendRequest"
    />
  </tr>
</template>

<script>
export default {
  name: "ActionItem",
  emits: ["request"],
  props: {
    node: {
      type: Object,
      required: true,
    },
    spacing: {
      type: Number,
      default: 0,
    },
  },
  data() {
    return {
      showChildren: false,
    };
  },
  computed: {
    nodeMargin() {
      return {
        "padding-left": `${this.spacing}px`
      };
    },
    hasChildren() {
      const { children } = this.node;
      return children && children.length > 0;
    },
  },
  methods: {
    sendRequest(node, hasChildren) {
      if (hasChildren) this.toggleChildren();
      else this.$emit("request", node);
    },
    toggleChildren() {
      this.showChildren = !this.showChildren;
    },
  },
};
</script>

<style>
</style>