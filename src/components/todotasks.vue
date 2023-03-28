<template>
    <div class="tasks-list-container">
  <h2>Estas são as suas tarefas:</h2>

<table class="content-table">
<tbody >
        <tr v-for="task in tasks" :key="task.name">
            <td>{{ task.name }}</td>
            <td><button class="remove-btn" @click="deleteTask(task.id)">X</button></td>
        </tr>   
</tbody> 
</table>
</div>
</template>
<script>
export default{
    name: "todotasks",
    data(){
        return{
            tasks: null
        }
    },
    methods:{
        async getTasks(){
            const req = await fetch("http://localhost:3000/tasks")

            const data = await req.json()

            this.tasks = data
            console.log(this.tasks)
        },
        async deleteTask(id){
            const req = await fetch(`http://localhost:3000/tasks/${id}`,{
                method: "DELETE"
            })
            const res = await req.json()

            this.getTasks()
        }

    },
    mounted(){
        this.getTasks()
    }
}
</script>
<style scoped>
#task-list{
    list-style: none;
    padding-left: 0;
}

#task-list li{
    text-align: left;
    height: 50px;
    line-height: 50px;
    position: relative;
    border-bottom: 3px solid #34073d;
    background-color: #fff;
    color: #34073d;
    margin-bottom: 10px;
    padding-left: 15px;
    transition: .5s;
    font-weight: bold;
}

#task-list button{
    position: absolute;
    top: 0;
    height: 40px;
    transition: .5s;
    cursor: pointer;
    width: 30px;
    padding: 5px;
}

button:focus{
    outline: none;
}


.remove-btn{
    transition:  .5s;
    width: 100%;
    height: 100%;
    right: 0px;
    padding: 5px;
    background-color: #fff;
    border: none;
}
.remove-btn:hover{
    color: #ffff;
    background-color: #eb0927;
    outline: none;
    border: none;
}
.content-table{
            border-collapse: collapse;
            margin: 25px 0;
            font-size: 0.9em;
            min-width: 400px;
            overflow: hidden;
        }
        .content-table td{
            padding: 10px 0px;
        }
        .content-table tbody tr{
            border-bottom: 1px solid #280068dd;
        }

        .content-table tbody tr:last-of-type{
            border-bottom: 2px solid #003098;
        }
        .content-table tbody tr.active-row{
            font-weight: bold;
            color: #ecf2ff;
        }
</style>