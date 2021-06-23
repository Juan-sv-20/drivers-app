<template>
  <div class="bar">
    <div class="bar_button" @click="createNewGroup()">
      <span>New Group</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "bar",
  methods: {
    createNewGroup() {
      this.$emit("createNewGroup", 1);
    },
  },
};
</script>

<style lang="scss" scoped>
.bar {
  display: grid;
  height: 50px;
  justify-items: left;

  &_button {
    background-color: #21b9ff;
    border-radius: 9px;
    margin: 4px 10px;
    width: 100px;
    height: 80%;
    display: grid;
    align-items: center;
    color: white;
  }
  &_button:hover {
    background-color: #1ba2e0;
    cursor: pointer;
  }
}
</style>
