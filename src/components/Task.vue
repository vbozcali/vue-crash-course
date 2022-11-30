<template>
    <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
        <div class="content">
            <h3>{{ task.text }}</h3>
            <p>{{ task.day }}</p>
        </div>
 
        <i @click="$emit('delete-task', task.id)" class="fas fa-trash"></i>  
    </div>
</template> 

<script>
export default {  
    name: 'Task', 
    props: {
        task: Object
    }
}
</script>

<style scope>
.task {
    display: flex;
    max-width: 100%;
    align-items: center;
    background-color: #F5F5F5;
    padding: 5px 15px;
    border: 1px solid #B8B8B8;
    margin-bottom: 10px;
}

.task i {
    margin-left: auto;
    color: red;
}

 .task content {
    display: flex;
    flex-direction: column;
    align-items: baseline;
}

.reminder {
    border-left: 5px solid green;
}
</style>