<template>
    <div>
        <form v-on:submit="submitData">
            <input type="text" 
                   name="title" 
                   placeholder="Add what you want to do..."
                   v-model="title">
            <input type="submit" 
                   value="Add" 
                   class="btn">
        </form>
    </div>
</template>

<script>

export default {
    name:"AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        submitData(e) {
            e.preventDefault();

            const newTodo = {
                title: this.title,
                completed: false,
            } 
            
            this.$emit('add-todo', newTodo);

            this.title = '';
        }
    }
}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }
    
    input[type="submit"] {
        flex: 2;
    }

    .btn {
        background: grey;
    }
</style>