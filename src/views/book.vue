<template>
  <section class="main">
    <BookRoom v-if="current === 'book'" />
    <LookForRoom v-if="current === 'select'" />
  </section>
</template>

<script>
import BookRoom from "../components/RoomBook/BookRoom";
import LookForRoom from "../components/RoomBook/LookForRoom";

export default {
  name: "BookRoom",
  components: {
    BookRoom: BookRoom,
    LookForRoom: LookForRoom,
  },
  data() {
    return {
      current: "select",
    };
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
