<template>
    <div>
        <form @submit.prevent="submitData">
            <label for="task"></label>
            <input name="task" type="text" v-model="input">
            <button>Add task</button>
        </form>
    </div>
</template>

<script>
export default{
    //emits:['inputValue'],
    data(){
        return{
            input:''
        }
    },methods:{
        submitData(){
            this.$emit('inputValue',this.input);
            this.input ='';
        }
    }
}
</script>