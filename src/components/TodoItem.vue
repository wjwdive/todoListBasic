<template>
    <li>
        <label>
            <input type="checkbox" :checked='todo.done' @change="toggleCheck(todo.id)" />
            <span>{{ todo.title }}</span>
        </label>
        <button class="btn btn-danger" @click="deleteItem(todo.id)">删除</button>

        <!-- <input type="checkbox" :checked='todo.done' @change="toggleCheck(todo.id)"/> <span>{{todo.title}} <button>删除</button></span> -->
        <!-- 这里可以用v-model 绑定,但是不建议. vue对props是浅监视。在第一层对象直接改会报错，绑定在对象里的值用v-model绑定vue不会报错 -->
        <!-- <input type="checkbox" v-model="todo.done"/> <span>{{todo.title}} <button>删除</button></span> -->

    </li>
</template>

<script>
export default {
    name: "TodoItem",
    data() {
        return {

        }
    },
    //声明 接收todo对象
    props: ['todo', 'toggleTodo', 'deleteTodo'],
    methods: {
        //切换选中
        toggleCheck(id) {
            //通知App组件，将对应的todo.done 改变【数据在哪里，数据的操作改变也应该在哪里】
            this.toggleTodo(id)
        },
        //删除
        deleteItem(id) {
            if (confirm('你确定要删除此条目吗？')) {
                console.log(id)
                //通知App vue 删除一个vue
                this.deleteTodo(id)
            }
        }
    }

}
</script>

<style scoped>
li {
    height: 30px;
}
li button {
    float: right;
    display: none;
    margin-top: 3px;
}
li:hover {
    background: skyblue;
}

li:hover button {
    display: block;
}
</style>