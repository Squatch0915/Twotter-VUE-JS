<!--Template is the HTML portion -->
<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{user.username}}</h1>
      <div class="user-profile_adminBadge" v-if="user.isAdmin">
        Admin
      </div>
      <div class="user-profile_follower-count">
        <strong>Followers:</strong> {{followers}}
      </div>
      <!-- Create event to take place using submit.prevent -->
      <form class="user-profile_create-twoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4" v-model="newTwootContent"/>

            <!-- The value of the option is dynamic and it depends on the option
          we're currently iterating in, in the twootTypes list.
          The option is the object here. -->
        <div class="user-profile_create-twoot-type">
          <label for="newTwootType"><strong>Type:</strong></label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option :value="option.value" v-for="(option, index) in twootTypes" :key="index">
              {{option.name}}
            </option>
          </select>
        </div>

        <button class="buttonClass">
          Twoot!
        </button>
      </form>
    </div>   
    <div class="user-profile_twoots-wrapper">
      <!--Loop to create a TwootItem Component for each twoot in the list
      and pass the props for username, and the twoot object 
      the twoot object, is being pulled from 'v-for=twoot'
      @favorite is the event we're emitting up to the parent from child-->
      <TwootItem 
      v-for="twoot in user.twoots" 
      :key="twoot.id" 
      :username="user.username" 
      :twoot="twoot"
      @favorite="toggleFavorite"
      />
    </div>   
 </div> 
</template>


<script>
//Importing the TwootItem.vue file into UserProfile, to access twoots
//and other data.
import TwootItem from "./TwootItem";

export default {
  name: 'UserProfile',
  components: {TwootItem},
  data(){
    return{

      newTwootContent: '',
      selectedTwootType: 'instant',
      //array of twoot types, that are objects
      twootTypes:[
        {value: 'draft', name: 'Draft'},
        {value: 'instant', name: 'Instant Twoot'}

      ],
      followers: 0, 
      user: {
        id: 1, 
        username: 'Wandering.Squatch',
        firstName: 'Jonathan', 
        lastName: 'Rogers', 
        email: 'jlrogers915@gmail.com',
        isAdmin: true, 
        //Creating an array of twoots
        twoots: [
          {id:1, content: 'Twotter is amazing!'}, 
          {id:2, content: "Don't forget to subscribe!"}
        ]
      }
    }
  },
  //Watches DataPoint, and when it changes it runs a function.  
  watch:{
    follwer(newFollowerCount, oldFollowerCount){
      if(oldFollowerCount < newFollowerCount){
        console.log(` ${this.user.username} has gained a follower! `);
      }
    }
  },

  computed:{
    fullName(){

      return `${this.user.firstName} ${this.user.lastName}`;
    }
  },

  methods: {
    followUser(){
      this.followers++;
    }, 

    //pass id in
    toggleFavorite(id){
      console.log(`Favorited Twoot #${id}`)
    },

    //Check to make sure it is not a twoot draft
    //if NOT, add new twootContent to the top of the twoot list using unshift. 
    //using an iteration of twoot length to get ID's, normally handled by DB
    createNewTwoot(){
      if(this.newTwootContent && this.selectedTwootType !== 'draft'){
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent
        })
        // Clears box after hitting submit
        this.newTwootContent = '';
      }

    }

  },
  //This is run basically at the start of the page.  Therefore it increased the follower count
  //by 1, because it calls the followUser method at startup. 
  mounted(){
    this.followUser();
  }
}
</script>

<!--Template is the CSS portion 
Using scoped means that it only applies to this specific component-->
<style scoped>

.user-profile{
display: grid;
grid-template-columns: 1fr 3fr;
width: 100%;
padding: 50px 5%;
}

.user-profile_user-panel{
display: flex;
flex-direction: column;
margin-right: 50px;
padding: 20px;
background-color: white;
border-radius: 5px;
border: 1px solid #DFE3E8;
}

h1{
  margin: 0;
}


.user-profile_adminBadge{
background:seagreen;
color: white;
border-radius: 5px;
margin-right: auto;
padding: 8px;
}

.user-profile_create-twoot{
padding-top: 20px;
display: flex;
flex-direction:  column;

}

.buttonClass{

  border-radius: 10px;
  width: 50%;
  background-color:darkolivegreen;
  color: white;
  margin-top: 10px;
  margin-left: 175px;
}


</style>
