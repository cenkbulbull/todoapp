<template>
  <nav class="filter-nav">
      <button @click="updateFilter('all')" :class="{active:activeTab==='all'}" >Tüm Görevler</button>
      <button @click="updateFilter('completed')" :class="{active:activeTab==='completed'}">Tamamlanan Görevler</button>
      <button @click="updateFilter('continues')" :class="{active:activeTab==='continues'}">Devam Eden Görevler</button>
  </nav>
</template>

<script>
export default {
    props:['activeTab'],
    methods:{
        updateFilter(status){
            this.$emit('filterStatus',status)
        }
    }
}
</script>

<style>

.filter-nav button {
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
  }
  .filter-nav button.active {
    color: #b33939;
  }
</style>