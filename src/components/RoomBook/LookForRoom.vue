<template>
  <div class="section">
    <h2>Select date and time</h2>
    <div class="screen">
      <form @submit.prevent>
        <div class="input-selection">
          <input type="date" name="date" id="date" v-model="date" />
          <label for="date">Select date:</label>
        </div>
        <div class="input-selection">
          <input
            type="time"
            name="from-time"
            id="from-time"
            v-model="timefrom"
          />
          <label for="from-time">From:</label>
        </div>
        <div class="input-selection">
          <input type="time" name="to-time" id="to-time" v-model="timeto" />
          <label for="to-time">To:</label>
        </div>
        <button type="submit" @click="submit" :disabled="validated">
          Check
        </button>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  name: "BookRoom",
  data() {
    return {
      current: "select",
      timefrom: "",
      timeto: "",
      date: "",
    };
  },
  computed: {
    validated() {
      if (this.timefrom === "" || this.timeto === "" || this.date === "") {
        return true;
      } else {
        return false;
      }
    },
  },
  methods: {
    submit() {
      //convert dates to milliseconds
      let selected_date = new Date(this.date);
      //convert seleted date and time to milliseconds
      let selected_to_milliseconds =
        selected_date.getTime() +
        1000 * 60 * 60 * this.timefrom.split(":")[0] +
        1000 * 60 * this.timefrom.split(":")[1] -
        1000 * 60 * 60;
      let today_date = new Date();
      let today_to_milliseconds = today_date.getTime();

      //check if selected time is correct
      if (this.timefrom > this.timeto) {
        return alert("Incorrect time");
      }
      //check if date is correct
      else if (selected_to_milliseconds < today_to_milliseconds) {
        return alert("Incorrect date");
      }

      alert("all good here!");
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.section {
  position: absolute;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  background-color: lightgray;
}

.section .screen {
  position: relative;
  height: 300px;
  width: 70%;
  border-radius: 5%;
  box-shadow: 2px 2px 30px black;
  background-color: gray;
}

.input-selection {
  position: relative;
  display: flex;
  flex-direction: column;
  flex-direction: column-reverse;
  gap: 10px;
  margin: 10px;
}

.input-selection label {
  color: white;
  font-size: 14px;
  font-weight: 500;
  transition: 0.5s;
}

.input-selection input {
  border-radius: 10px;
  border: none;
  padding: 2px 5px;
  font-size: 14px;
  background-color: lightgray;
  cursor: pointer;
  transition: 0.5s;
}

.input-selection input:hover {
  border: 1px solid black;
}

.input-selection input:focus {
  border: 1px solid black;
  background-color: white;
  font-size: 16px;
}

.input-selection input:focus + label {
  font-size: 16px;
}

button[type="submit"] {
  margin: 30px 0;
  border-radius: 10px;
  box-shadow: 1px 1px 15px black;
  font-size: 14px;
  padding: 5px 15px;
  border: none;
  cursor: pointer;
  transition: 0.5s;
}

button[type="submit"]:hover:not(button[type="submit"]:disabled) {
  background-color: blue;
  padding: 8px 18px;
  color: white;
}

form {
  margin: 20px 0;
}
</style>
