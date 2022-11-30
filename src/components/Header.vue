<template>
    <header>
        <h1> {{ title}} </h1>

        <Button @toggle-add-task="$emit('toggle-add-task')" :color="showAddTask ? 'danger' : 'primary'" :text="showAddTask ? 'Close' : 'Add Task' " />
    </header>
</template>

<script>  
    import Button from './Button.vue';

    export default {
        name: 'Header',

        /* Usage 1
            props: ['title']
        */

       // Usage 2 - As an object
       props: {
        title: {
            type: String,
            default: 'Hello World'
        },
        showAddTask: {
            type: Boolean
        }
       },

       // Components
       components: {
        Button
       }
    }
</script>

<style scoped> 
    header {
        display: flex;
        align-items: center;
    }

    header h1 {
        margin-right: 15px;
    }
</style>