<template>
    <header>
        <h1>{{ title }}</h1>
        <Button @btn-click="$emit('btn-click')" :text="showBtn? 'close':'Add Task'" :color="showBtn? 'red' : 'green'"/>
    </header>
    </template>

<script>
    import Button from './Button'
    export default{
        name: 'Header',
        props: {
            title: String,
            showBtn:Boolean
        },
        components: {
            Button,
        }
    }
</script>

<style scoped>
    header{
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>

<!-- <template>
    <header>
      <h1>{{ title }}</h1>
      <Button/>
    </header>
  </template> -->