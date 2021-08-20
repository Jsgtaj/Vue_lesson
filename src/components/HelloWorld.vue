<template>
  <div class="hello">
    <p>{{ fName }} {{ lName }}</p>
    <p>Age: {{ age }}</p>
    <p>{{ country }}</p>
    <img v-bind:src="img" />
  </div>
</template>

<script>
export default {
  name: "HelloWorld",

  data() {
    return {
      fName: null,
      lName: null,
      age: null,
      country: null,
      img: null,
    };
  },
  created() {
    this.fetchJSON();
  },
  methods: {
    fetchJSON() {
      //redefine this inside the method
      const vm = this;
      const url = "https://randomuser.me/api/";
      fetch(url)
        .then((resp) => resp.json())
        .then(function (data) {
          vm.fName = data.results[0].name.first;
          vm.lName = data.results[0].name.last;
          vm.age = data.results[0].dob.age;
          vm.country = data.results[0].location.country;
          vm.img = data.results[0].picture.large;
        })
        .catch(function (err) {
          console.log(err);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
