<template>
    <h1>Edit Form</h1>
    <form @submit.prevent="addProject">
    <label>Project Title</label>
    <input type="text" v-model="title">

    <label>Project Detail</label>
    <input type="text" v-model="detail">

     <button @click="updateProject">Update Project</button>

  </form>
</template>

<script>
export default {
    props:["id"],
    data(){
        return{
            title:"",
            detail:""
        }
    },
    mounted(){
        fetch("http://localhost:3000/projects/"+this.id) //fetch return default get method
        .then((response)=>{
            return response.json();
        })
        .then((datas)=>{
            this.title = datas.title
            this.detail = datas.detail
        })
        .catch((err)=>{
            console.log(err);
        })
    },
    methods:{
        updateProject(){
            fetch("http://localhost:3000/projects/"+this.id,{
                method:"PATCH",
                headers:{
                    "Content-type":"application/json"
                },
                body:JSON.stringify(
                    {
                    title : this.title,
                    detail : this.detail
                }
                )
            })
            .then(()=>{
                return this.$router.push("/")
            })
            .catch((err)=>{
                console.log(err)
            })
        }
    }
}
</script>

<style>

</style>