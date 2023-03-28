<template>
<div id="tasks-header">
<h2>Salve a sua próxima tarefa:</h2>
<form id="add-task-form" @submit="createTask">
    <input type="text" name="task" v-model="name" id="task-title" placeholder="O que você vai fazer?">
    <button id="add-btn" type="submit">+</button>
</form>
</div>
</template>
<script>
export default{
    name: "formtodo",
    data(){
        return{
            name: null,
            completed: false 
        }
    },
    methods:{
        async createTask( ){
            const data ={
                name: this.name,
                completed: this.completed
            }

            const dataJson = JSON.stringify(data)

            const req = await fetch("http://localhost:3000/tasks", {
                method: "POST",
                headers: { "Content-Type": "application/json"},
                body: dataJson
            })
            const res = await req.json()

            this.name = ""

        }
    }
}
</script>

<style scoped>
#task-title{
    box-sizing: border-box;
    border: 1px solid #34073d;
    background-color: #fff;
    color: #34073d;
    padding: 15px;
    font-size: 18px;
    width: 100%;
}
#add-task-form input:focus{
    outline: none;
}

#add-task-form input::placeholder{
    color: #003098;

}
#add-btn{
    position: absolute;
    font-size: 30px;
    background-color: #fff;
    border: 1px solid #34073d;
    cursor: pointer;
    transition: .5s;
    width: 60px;
    height: 53px;
    padding-top: 3px;
}
#add-btn:hover{
    background-color: #003098;
    color: #FFF;
}
</style>