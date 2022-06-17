<template>
  <body>
    <!-- <header>
      <h1>METAR/TAF</h1>
    </header> -->

    <img alt="Vue logo" src="./assets/metar_taf.png" />
    <!-- <HelloWorld msg="Create a quick printable list of metar/taf reports" /> -->
    <h2>Create a quick printable list of metar/taf reports.</h2>

    <section id="entry">
      <h2>Add ICAO identifier (ie. KSEA)</h2>
      <!-- use enter key+button -->
      <input type="text" v-model="enteredTask" @keyup.enter="addTask" />
      <button @click="addTask">Add ID</button>
      <p></p>
      <button @click="showhide">{{ buttonCaption }}</button>
      <p v-if="enteredTask.length > 4">Not a valid ID</p>
      <p v-if="airports.length === 0">No IDs have been added yet</p>
      
      <!-- previously <ul v-else> -->
      <p v-else>
        <ul v-if="showlist">
          <li
            v-for="(airports, index) in airports"
            v-bind:key="index"
            @click="removeTask(index)"
          >id: {{ airports }}
          </li>
        </ul>
      </p>
      <!-- <button @click="showhide">{{ buttonCaption }}</button> -->
    </section>


<p>-------</p>

        <ul v-if="showlist">
          <li
            v-for="(airports, index) in airports"
            v-bind:key="index"
            @click="removeTask(index)"
          >id: {{ airports }}
          </li>
        </ul>
   


  </body>
</template>

<script>
export default {
  data() {
    return {
      enteredTask: "",
      airports: [],
      showlist: true,
      reports: [],
    };
  },

  computed: {
    buttonCaption() {
      return this.showlist ? "Hide" : "Show";
    },
  },

  methods: {
    addTask() {
      this.airports.push(this.enteredTask);

      // use metar/taf API and store in 'report'
      // 'get' api with 'enteredTask'


      // this.reports.push(this.report);

      

      // clear input:
      this.enteredTask = "";
    },

    removeTask(idx) {
      this.airports.splice(idx, 1);
    },

    showhide() {
      this.showlist = !this.showlist;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

* {
  box-sizing: border-box;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(87, 87, 87, 0.26);
  margin: 3rem;
  border-radius: 10px;
  padding: 1rem;
  background-color: #000000;
  color: white;
  text-align: center;
}

h2 {
  font-size: 1rem;
  border-bottom: 4px #ccc;
  color: #1e3034;
  margin: 0 0 1rem 0;
}

li {
  list-style-type: none;
  margin: 1rem 0;
  font-size: 1.25rem;
  font-weight: normal;
  background-color: #9a9a9a;
  padding: 0.5rem;
  color: #ffffff;
  border-radius: 2px;
}

input {
  font: inherit;
  border: 1px solid #ccc;
}

input:focus {
  outline: none;
  border-color: #000000;
  background-color: #d7fdeb;
}

button {
  font: inherit;
  cursor: pointer;
  border: 1px solid #000000;
  background-color: #3f72ff;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

button:hover,
button:active {
  background-color: #8eacff;
  border-color: #000000;
  box-shadow: 1px 1px 4px rgba(87, 87, 87, 0.26);
}
</style>
