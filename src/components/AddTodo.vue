<template>
    <div>
        <form @submit="addTodo">
            <input v-model="title" type="text" name="title" placeholder="Add Todo...">
            <input class="btn" type="submit" value="Submit" >
        </form>
    </div>
</template>

<script>
export default {
    name:"AddTodo",
    data(){
        return{
            title:'',
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault();
            const newTodo = {
                title:this.title,
                completed:false,
            }
            //this should be sent to parent
            this.$emit('add-todo',newTodo);
            this.title = '';
        }
    }
}
</script>
<style scoped>
    form{
        display: flex;
    }
    input[type='text']{
          flex: 10;
          padding: 10px;  
    }
    input[type=submit]{
        flex: 2;
    }
</style>