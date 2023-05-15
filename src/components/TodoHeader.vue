<template>
    <header class="header">
        <h1>todos</h1>
        <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll">
        <label for="toggle-all"></label>
        <input class="new-todo" placeholder="输入任务名称-回车确认" autofocus @keydown.enter="addTask" v-model="task" />
    </header>
</template>
  
<script>
export default {
    props: ['Harr'],
    data() {
        return {
            task: ''
        }
    },
    methods: {
        addTask() {
            if (this.task.trim().length === 0) {
                alert('内容不能为空!');
                return;
            }
            this.$emit("addTaskApp", this.task);
            this.task = "";
        }
    },
    computed: {
        isAll: {
            set(selected) {
                this.Harr.forEach(obj => obj.isDone = selected);
            },
            get() {
                return this.Harr.length !== 0 && this.Harr.every(obj => obj.isDone === true);
            }
        }
    }
}
</script>