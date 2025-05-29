<script setup>
defineProps({
   
})
</script>

<template>
    <form @submit.prevent="addComment" class="container col-md-5">
        <div class="mb-3">
            <label for="inputName" class="form-label">{{ labelName }}</label>
            <input v-model="valueName" type="text" class="form-control" name="inputName" id="inputName" data-v-inspector="input-email">
        </div>
        <div class="mb-3">
            <label for="inputComment" class="form-label">{{ labelComment }}</label>
            <textarea v-model="valueComment" class="form-control" name="inputComment" id="inputComment" ></textarea>
            <div class="mt-2">
                <p class="text-danger">{{ erro }}</p>
            </div>
        </div>
        <div class="d-flex mt-3 gap-2">
            <button type="reset" class="btn btn-warning">Clear</button>
            <button type="submit" class="btn btn-primary">Submit</button>
        </div>
    </form>

    <div class="container col-md-5 mt-5 list-group">
        <ul class="list-group-flush px-0 border h-50">
            <li class="list-group-item px-0 mx-4" v-for="(item, index) in comments" :key="index">
                <div class="d-flex justify-content-between align-items-center">
                    <div class="fw-bold">
                        {{ item.name }}
                        <p>{{ item.comment }}</p>
                    </div>
                    <div class="float-end">
                        <button @click="deleteComment(index)" class="btn btn-danger my-auto">
                            Delete
                        </button>
                    </div>
                </div>
            </li>
        </ul>
    </div>

</template>



<script>
  export default{
    data(){
        return {
            labelName: "Your Name",
            labelComment: "Your Comment",

            valueName:"",
            valueComment: "",
            erro:"", 

            comments: [{"name": "User 1", "comment": "I like"}, {"name": "User 2", "comment": "I do not like"}]
        }
        
    },
    
    methods: {
        addComment(){
            if (this.valueName == ""){
                this.erro = "What's yr name?"
                return ;
            }
            
            if (this.valueComment.trim().length === 0){
                this.erro = "What's yr comment?"
                return ;
            }
            
            this.comments.push({
                "name":this.valueName,
                "comment":this.valueComment
            })

            this.erro="";
            this.valueName = "";
            this.valueComment = "";

       }
    }
  }

</script>

