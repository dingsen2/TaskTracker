<template>
    <header>
        <h1>{{ title }}</h1>
        <Button v-show="homePage" @btn-click="$emit('btn-click')" :text="showBtn? 'close':'Add Task'" :color="showBtn? 'red' : 'green'"/>
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
        },
        computed: {
            homePage() {
                if(this.$route.path === '/') {
                    return true
                }
                else{
                    return false
                }
            }
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