 <template>
    <button @click="$emit('toggle-add-task')" :class="['btn-' + color, 'btn']">{{ text }}</button>
 </template>

<script>
    export default {
        name: 'Button',
        props: {
            text: String,
            color: String
        }
    }
</script> 

<style>

</style>