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
    </div>   
    <div class="user-profile_twoots-wrapper">
      <!--Loop to create a TwootItem Component for each twoot in the list
      and pass the props for username, and the twoot object 
      the twoot object, is being pulled from 'v-for=twoot'-->
      <TwootItem v-for="twoot in user.twoots" :key="twoot.id" :username="user.username" :twoot="twoot"/>
    </div>   
 </div> 
</template>


<script>

export default {
  name: 'UserProfile',
  data(){
    return{
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

  },
  //This is run basically at the start of the page.  Therefore it increased the follower count
  //by 1, because it calls the followUser method at startup. 
  mounted(){
    this.followUser();
  }
}
</script>

<!--Template is the CSS portion -->
<style>

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

</style>
