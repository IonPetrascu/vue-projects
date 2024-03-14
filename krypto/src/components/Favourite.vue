<template>
  <h2>Варианты в избранном</h2>
  <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<script>
export default {
  props: {
    favs: {
      type: Array,
      required: true,
    },
    getFromFavs: {
      type: Function,
      required: true,
    },
  },
};
</script>

<style scoped>
div {
  display: flex;
  justify-content: space-between;
  width: 500px;
  margin: 0 auto;
  background-color: whitesmoke;
  border: 1px solid;
  padding: 5px;
  cursor: pointer;

}
span{
    background-color: rgba(211, 180, 211, 0.74);
    padding: 3px;
    
}
</style>
