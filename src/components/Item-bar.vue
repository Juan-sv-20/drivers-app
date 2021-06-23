<template>
  <div class="Item">
    <div class="Item_tittle">
      <input type="text" name="tittle" id="" :value="titulo" />
    </div>
    <div class="Item_components">
      <div class="Item_components-items">
        <select name="" id="">
          <option v-for="destino in Destinos" :key="destino" :value="destino">
            {{ destino }}
          </option>
        </select>
      </div>
      <div class="Item_components-items">
        <select name="" id="">
          <option v-for="destino in Destinos" :key="destino" :value="destino">
            {{ destino }}
          </option>
        </select>
      </div>
      <div
        class="Item_components-items"
        @mouseenter="showPriority()"
        @mouseleave="showPriority()"
      >
        <div
          class="Item_components-items-priority"
          v-bind:class="[Type]"
          v-bind:Style="Style_Priority"
          ref="Bus_Priority"
        >
          <span>{{ Priority[0] }}</span>
        </div>

        <!-- 
                        Ventana Modal para seleccionar la prioridad
                     -->

        <div
          class="ventana-modal"
          v-if="Ventana_Priority"
          v-bind:Style="setPositionPriority"
        >
          <div
            class="ventana-modal_item"
            v-for="item in Priorities"
            :key="item"
            v-bind:Style="'background:' + item[1]"
            @click="setPriority(item)"
          >
            <span>{{ item[0] }}</span>
          </div>
        </div>
      </div>
      <div
        class="Item_components-items"
        @mouseenter="showStatus()"
        @mouseleave="showStatus()"
      >
        <div
          class="Item_components-items-priority"
          v-bind:class="[Type]"
          v-bind:Style="Style_Status"
          ref="Bus_Status"
        >
          <span>{{ Statu[0] }}</span>
        </div>

        <!-- 
                        Ventana Modal para seleccionar la Status
                     -->

        <div
          class="ventana-modal"
          v-if="Ventana_Status"
          v-bind:Style="setPositionStatus"
        >
          <div
            class="ventana-modal_item"
            v-for="item in Status"
            :key="item"
            v-bind:Style="'background:' + item[1]"
            @click="setStatus(item)"
          >
            <span>{{ item[0] }}</span>
          </div>
        </div>
      </div>
      <div class="Item_components-items">
        <div class="Item_components-items-button" @click="removeItem()">
          <span>Remove</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "item-bar",
  props: {
    titulo: String,
  },
  data() {
    return {
      Destinos: [
        "Shipping",
        "Receiving",
        "PackShed 2",
        "Furukuawa",
        "Bonipack",
        "Erick's Yard",
      ],
      Priority: ["Default", "#7d807e"],
      Priorities: [
        ["High", "#e00034"],
        ["Medium", "#f5b82a"],
        ["Low", "#00cf2d"],
        ["Default", "#7d807e"],
      ],
      Statu: ["Default", "#7d807e"],
      Status: [
        ["Stuck", "#e00034"],
        ["Working on it", "#f5b82a"],
        ["Done", "#00cf2d"],
        ["Default", "#7d807e"],
      ],
      Type: "Item-Group",
      Ventana_Priority: false,
      Ventana_Status: false,
      posicion: [0, 0],
    };
  },
  methods: {
    removeItem() {
      this.$emit("removeItem", this.titulo);
    },
    setPriority(item) {
      this.Priority = item;
      this.Ventana_Priority = !this.Ventana_Priority;
    },
    setStatus(item) {
      this.Statu = item;
      this.Ventana_Status = !this.Ventana_Status;
    },
    showPriority() {
      this.posicion[0] = this.$refs["Bus_Priority"].getBoundingClientRect().x;
      this.posicion[1] = this.$refs["Bus_Priority"].getBoundingClientRect().y;
      this.Ventana_Priority = !this.Ventana_Priority;
    },
    showStatus() {
      this.posicion[0] = this.$refs["Bus_Status"].getBoundingClientRect().x;
      this.posicion[1] = this.$refs["Bus_Status"].getBoundingClientRect().y;
      this.Ventana_Status = !this.Ventana_Status;
    },
  },
  computed: {
    Style_Priority() {
      return "background: " + this.Priority[1];
    },
    Style_Status() {
      return "background: " + this.Statu[1];
    },
    setPositionPriority() {
      return "left: " + this.posicion[0] + "; top: " + this.posicion[1] + ";";
    },
    setPositionStatus() {
      return "left: " + this.posicion[0] + "; top: " + this.posicion[1] + ";";
    },
  },
};
</script>

<style lang="scss" scoped>
.Item-Group {
  color: white;
}

input {
  border-width: 0;
  border: none;
  outline: 0;
  width: 99%;
}
input:focus {
  outline: none !important;
}

.Item {
  display: grid;
  grid-template-columns: 40% auto;
  padding: 5px;

  &_tittle {
    display: grid;
    justify-items: left;
  }

  &_tittle:hover {
    border: 1px solid #21b9ff;
  }

  &_components {
    display: grid;
    grid-template-columns: 20% 20% 20% 20% 20%;
    justify-items: center;

    &-items {
      display: grid;
      justify-items: Center;
      align-items: center;
      padding: 4px;
      width: 95%;

      &-priority {
        display: grid;
        justify-items: Center;
        align-items: center;
        width: 100%;
        height: 100%;
      }

      &-priority {
        cursor: pointer;
      }

      select {
        width: 100%;
        border-width: 0;
        border: none;
        outline: 0;
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        font-weight: bold;
        font-size: 15px;
      }
      select:focus {
        outline: none !important;
      }

      &-button {
        background: #e00034;
        padding: 7px;
        border-radius: 10px;
        width: 75px;
        color: white;
      }
      &-button:hover {
        background-color: #b3022b;
        cursor: pointer;
      }
    }
    &-items:hover {
      outline: 1px solid #21b9ff;
    }
    &-items:last-child:hover {
      outline: none !important;
    }
  }
}

.ventana-modal {
  position: fixed;
  width: 150px;
  background-color: #bfbdbd;

  &_item {
    height: 25px;
    cursor: pointer;
    padding: 5px;
    margin: 5px;
    display: grid;
    justify-items: center;
    align-items: center;
    color: white;
  }
}
</style>
