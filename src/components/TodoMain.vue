<template>
    <ul class="todo-list">
        <!-- completed: 完成的类名 -->
        <!-- complete类名: 完成后任务，画横线，代表已完成 -->
        <li :class="{completed: obj.isDone}" v-for="(obj, index) in arr" :key="obj.id">
            <div class="view">
                <!-- 打勾后，代表已完成任务，赋值给obj.isDone -->
                <input class="toggle" type="checkbox" v-model="obj.isDone"/>
                <label>{{ obj.name }}</label>
                <button class="destroy" @click="deleteTask(obj.id)"></button>
            </div>
        </li>
    </ul>
</template>
  
<script>
export default {
    props: ['arr'],
    methods: {
        deleteTask(taskId) {
            this.$emit('deleteTaskApp', taskId);
        }
    }
}
</script>