<template>
  <div>
    <div class="todoapp">
      <!-- :arr： arr自定义变量名字尽量别重复 -->
      <TodoHeader @addTaskApp="addTaskFun" :Harr="showArr"></TodoHeader>
      <TodoMain :arr="showArr" @deleteTaskApp="deleteTaskFun"></TodoMain>
      <TodoFooter :arr="showArr" @stateSwitchDataApp="selectedSwitchDataFun" @clearTaskApp="clearTaskFun"></TodoFooter>
    </div>
  </div>
</template>

<script>
import './styles/base.css';
import './styles/index.css';
import TodoHeader from './components/TodoHeader.vue';
import TodoMain from './components/TodoMain.vue';
import TodoFooter from './components/TodoFooter.vue';
export default {
  data() {
    return {
      chooseSelected: 'all',
      list: JSON.parse(localStorage.getItem('data')) || [],
    };
  },
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter
  },
  methods: {
    addTaskFun(task) {
      let id = this.list.length === 0 ? 100 : this.list[this.list.length - 1].id + 1;
      this.list.push({
        id: id,
        name: task,
        isDone: false
      });
    },
    deleteTaskFun(taskId) {
      let index = this.list.findIndex(obj => obj.id === taskId);
      this.list.splice(index, 1)
    },
    selectedSwitchDataFun(selected) {
      this.chooseSelected = selected;
    },
    clearTaskFun() {
      this.list = this.list.filter(obj => obj.isDone !== true);
    }
  },
  computed: {
    showArr() {
      if (this.chooseSelected === 'no') {
        return this.list.filter(obj => obj.isDone === false);
      } else if (this.chooseSelected === 'yes') {
        return this.list.filter(obj => obj.isDone === true);
      } else {
        return this.list;
      }
    }
  },
  watch: {
    list: {
      deep: true,
      handler() {
        localStorage.setItem('data', JSON.stringify(this.list));
      }
    }
  }
}
</script>

<style lang="scss" scoped></style>