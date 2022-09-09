<template>
  <li>
    <h2>{{name}} {{isFavorite? '(favorite)':''}}</h2>
    <button @click="toggleFavorite">Favorite</button>
    <button @click="toggleDetails">{{detailsAreVisible ? 'Hide' : 'Show'}} Details</button>
    <ul v-if="detailsAreVisible">
        <li><strong>Phone:</strong>{{phoneNumber}}</li>
        <li><strong>Email:</strong>{{emailAddress}}</li>
    </ul>
    <button @click="$emit('delete',id)">Delete</button>
  </li>
</template>
//working with git to get this published
<script>
export default {
    emits:['toggle-favorite','delete'],
    // emits: {
    //     'toggle-favorite':function(id){
    //         if(id){
    //             return true;
    //         }else{
    //             warn('id is missing biatch')
    //             return false;
    //         }
    //     }
    // },
    
    props:{
        id: {
            type: String,
            required: true,
        },
        name:{
            type:String,
            required:true,
        },
        phoneNumber:{
            type: String,
            required: true,
        },
        emailAddress: {
            type: String,
            required: true
        },
        isFavorite: {
            type: Boolean,
            required: false,
            default:false,
          
        },

    },
    data(){
        return{
            
            detailsAreVisible: false,
        }  
    },
    methods: {
        toggleDetails(){
            this.detailsAreVisible = !this.detailsAreVisible;
        },
        // '$emit' to communicate an event with the parent file app.vue
         toggleFavorite(){
            this.$emit('toggle-favorite',this.id)
        }
        
    },   
    
};
</script>

