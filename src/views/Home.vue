<template>
  <div class="home">
    <Bar @createNewGroup="AddGroups"> </Bar>
    <br />
    <Groups v-for="group in groups" :key="group"> </Groups>
  </div>
</template>

<script>
// @ is an alias to /src
import Bar from "@/components/Tools-bar.vue";
import Groups from "@/components/Group-bar.vue";

export default {
  name: "Home",
  data() {
    return {
      groups: 0,
    };
  },
  components: {
    Bar,
    Groups,
  },
  methods: {
    AddGroups(value) {
      this.groups += value;
    },
  },
};
</script>
