<template>
    <footer class="footer">
        <span class="todo-count">剩余<strong>{{ arr.length }}</strong></span>
        <!-- 利用事件委托的形式来绑定事件获取所需要的状态 -->
        <ul class="filters" @click="chooseSelectedFun">
            <li>
                <a :class="{ selected: isChoose === 'all' }" href="javascript:;" @click="isChoose='all'">全部</a>
            </li>
            <li>
                <a :class="{ selected: isChoose === 'no' }" href="javascript:;" @click="isChoose='no'">未完成</a>
            </li>
            <li>
                <a :class="{ selected: isChoose === 'yes' }" href="javascript:;" @click="isChoose='yes'">已完成</a>
            </li>
        </ul>
        <button class="clear-completed" @click="clearTask">清除已完成</button>
    </footer>
</template>
  
<script>
export default {
    data() {
        return {
            // 定义这个三个值： all:全部， yes: 已完成，no: 未完成
            isChoose: 'all'
        }
    },
    props: ['arr'],
    methods: {
        // 利用事件委托的形式来绑定事件获取所需要的状态
        chooseSelectedFun() {
            this.$emit('stateSwitchDataApp', this.isChoose);
        },
        clearTask() {
           this.$emit('clearTaskApp');
        }
    }

}
</script>