<!-- This is the html created using vue. -->
<template>
    <div class="twoot-item" @click="favoriteTwoot(twoot.id)">
        <div class="user-profile_twoot">
            <div class="twoot-item_user">
                @{{username}}
            </div>
            <div class="twoot-item_cotent">
                {{twoot.content}}
            </div>
        </div>
    </div>
</template>

<!-- Cannot render Twoot component w/out this required information, which we set.
Props are passing data from Parent to Child.  -->
<script>
export default {
    name:"TwootItem",
    props:{
        username:{
            type: String, 
            required: true
        },
        twoot:{
            type: Object, 
            required: true
        }
    },

    methods: {
        //this references vue.  $emit is built in functionality, 'what is the event we're emitting?'
        favoriteTwoot(id){
            this.$emit('favorite', id);
        }

    }
};
</script>

<style lang="scss">

.twoot-item{
    padding: 20px;
    background-color: white;
    border-radius: 10px;
    border: 2px solid #DFE3E8;
    box-sizing: border-box;
    cursor: pointer;
    transition: all 0.25s ease;
    margin-bottom: 5px;

    .twoot-item_user{
    font-weight: bold;
    }

    &:hover{
    transform: scale(1.1, 1.1);
    }
}





</style>