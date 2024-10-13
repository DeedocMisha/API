<template>
  <div>
    <button class="but_1" v-on:keydown.enter="ping" v-on:dblclick="ping">ping</button>
    <input type="text" name="but1" v-model="but1Value" />
    <form name="quest">
      <select ref="mySelect">
        <option value="update">Обновить</option>
        <option value="attempt">Добавить</option>
      </select>
    </form>
    <button
      v-on:click="removenotes"
      :style="{ fontcolor: 'black' }"
      style="background-color: red; padding: 10px; border-radius: 20px"
    >
      Удалять записи
    </button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  data() {
    return {
      but1Value: "",
    };
  },
  methods: {
    removenotes() {
      this.but1Value = "";
    },
    ping() {
      const client = axios.create();
      client.get("http://127.0.0.1:8000/").then((response) => {
        // обновляем значение but1Value
        if (this.$refs.mySelect.value === "update") {
          this.but1Value = response.data.message;
        } else {
          this.but1Value += response.data.message;
        }
      });
    },
  },
};
</script>
