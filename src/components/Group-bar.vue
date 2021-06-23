<template>
  <div class="group-bar">
    <div class="group-bar_header">
      <div class="group-bar_header_tittle">
        <input
          type="text"
          name="tittle"
          id=""
          value=""
          placeholder="New Group"
        />
      </div>
      <div class="group-bar_header_components">
        <div class="group-bar_header_components-items">
          <input type="text" name="From" id="" value="From" placeholder="" />
        </div>
        <div class="group-bar_header_components-items">
          <input type="text" name="To" id="" value="To" placeholder="" />
        </div>
        <div class="group-bar_header_components-items">
          <input
            type="text"
            name="Priority"
            id=""
            value="Priority"
            placeholder=""
          />
        </div>
        <div class="group-bar_header_components-items">
          <input
            type="text"
            name="Status"
            id=""
            value="Status"
            placeholder=""
          />
        </div>
        <div class="group-bar_header_components-items-hide">
          <div class="group-bar_header_components-items-hide-button">
            <span>Remove</span>
          </div>
        </div>
      </div>
    </div>
    <div class="group-bar_body">
      <Item
        v-for="item in items"
        :key="item"
        @titulo="item"
        :titulo="item"
        @removeItem="removeItem"
      ></Item>
    </div>
    <div class="group-bar_footer">
      <div class="group-bar_footer_text">
        <input
          type="text"
          name="Add"
          id="Add"
          placeholder="+ Add"
          v-model="addText"
        />
      </div>
      <div class="group-bar_footer_button" @click="addItem()">
        <span>Add</span>
      </div>
    </div>
  </div>
</template>

<script>
import Item from "@/components/Item-bar.vue";

export default {
  name: "group-bar",
  data() {
    return {
      items: [],
      addText: "",
    };
  },
  components: {
    Item,
  },
  methods: {
    addItem() {
      if (this.addText != "") {
        this.items.push(this.addText);
        this.addText = "";
      }
    },
    removeItem(value) {
      const index = this.items.indexOf(value);
      if (index > -1) {
        this.items.splice(index, 1);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
input {
  border-width: 0;
  border: none;
  outline: 0;
  width: 99%;
}
input:focus {
  outline: none !important;
}

.group-bar {
  margin: 3em;
  padding: 1em;
  box-shadow: 0em 0.5em 1em #aaa;
  display: grid;
  grid-template-rows: 1fr auto 1fr;

  &_header {
    display: grid;
    grid-template-columns: 40% auto;

    &_tittle {
      display: grid;
      justify-items: left;
      font-family: "Roboto Slab", serif;
      input {
        text-align: left;
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        font-weight: bold;
        font-size: 15px;
      }
    }

    &_tittle:hover {
      border: 1px solid #21b9ff;
    }

    &_components {
      display: grid;
      grid-template-columns: 20% 20% 20% 20% 20%;

      &-items {
        display: grid;
        justify-items: left;
        padding: 4px;

        input {
          text-align: left;
          font-family: Avenir, Helvetica, Arial, sans-serif;
          -webkit-font-smoothing: antialiased;
          -moz-osx-font-smoothing: grayscale;
          font-weight: bold;
          font-size: 15px;
        }
      }
      &-items:hover {
        border: 1px solid #21b9ff;
      }

      &-items-hide {
        display: grid;
        justify-items: left;
        padding: 5px;

        &-button {
          background: white;
          padding: 7px;
          border-radius: 10px;
          width: 75px;
          color: white;
        }
      }
    }
  }

  &_footer {
    display: grid;
    justify-items: left;
    grid-template-columns: 1fr auto;
    padding: 5px 7px;

    &_text {
      display: grid;
      justify-items: left;
      width: 100%;
    }
    &_button {
      background: #21b9ff;
      padding: 7px;
      border-radius: 10px;
      width: 50px;
      color: white;
    }
    &_button:hover {
      background-color: #1ba2e0;
      cursor: pointer;
    }
  }

  &_footer:hover {
    outline: 1px solid #21b9ff;
  }
}
</style>
