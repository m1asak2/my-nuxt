<template>
  <div>
  <h1>Todoリスト</h1>
  <table>
    <tr><th>連番</th><th>内容</th><th>完了</th><th>追加日</th><th>操作</th></tr>
    <tr v-for="(task,index) in todos" :key="index">
    <td>{{index}}</td>
    <!-- <td v-for="(item,i) in task" :key="i">{{item}}</td> -->
    <td>{{task.title}}</td>
    <td><input type="checkbox" :checked="task.done" @change="toggle(index)"/>{{task.done}}</td>
    <td>{{format(task.created_at)}}</td>
    <td><button @click.prevent="remove(index)">削除</button></td>
    </tr>
  <tr>
    <td>新規</td>
    <td><input type="text" v-model="title"/></td>
    <td></td>
    <td><button @click.prevent="add">追加</button></td>
  </tr>
  </table>
  </div>  
</template>
<script>
export default {
  data(){
    return{
    todos:[
      {title:"歯磨き",done:false,created_at: new Date()},
      {title:"宿題",done:false,created_at: new Date()},
    ],
    title:"",
    }
  },
  methods:{
    format(date){
      return date.getFullYear()
      +'/'+(date.getMonth()+1)
      +'/'+date.getDate()
      +' '+date.getHours()
      +':'+date.getMinutes();
    },
    add(){
      if(this.title){
        this.todos.push({
          title:this.title,
          done:false,
          created_at:new Date()
        })
        this.title=null
      }
    },
    remove(index){
      // 指定した配列を削除
      this.todos.splice(index,1)
    },
    toggle(index){
      this.$set(this.todos[index],'done',!this.todos[index].done)
    }
  }
}
</script>

<style>
th,td{
  border:1px solid silver;
}
</style>

