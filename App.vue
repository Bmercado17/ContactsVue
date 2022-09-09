

<template>
   <section>
   <header><h1>My Friends</h1></header>
    <ul>
      <new-friend @add-contact="addContact"></new-friend>
      <!-- v-for doesnt need to be : or v-bind -->
      <!-- all the props are v-bind n pssdfrom friendCntct component
      that is the information we pass from chld compnnt to prent -->
        <friend-contact
        v-for="friend in friends"
        :key="friend.id"
        :id="friend.id"
        :name="friend.name"
        :phone-number="friend.phone"
        :email-address="friend.email"
        :autocapitalize="friend.isFavorite"
        :is-favorite="friend.isFavorite"
        @toggle-favorite="toggleFavoriteStatus"
        @delete="deleteContact"
        ></friend-contact>
        </ul>
   </section>
</template> 
<script>
export default {
   data(){
    return {
        friends: [
           {
           id: 'Manuel',
           name: 'Manuel Lorenz',
           phone: '0132 456 788', 
           email: 'Lorenz@localHost.com',
           isFavorite:false
           }, 
           {
           id: 'Mari',
           name: 'Maribel',
           phone: '555 444 77777', 
           email: 'Mari@localHost.com',
           isFavortie:true
           }, 
        ]
    }
   },
  //  this  method is emited from FrndContact toggleFavoriteStatus
  //  argument this.id is to specify whc frnd is passd as friendId on method below
   methods: {
    toggleFavoriteStatus(friendId){
    let identifiedFriend = this.friends.find((friend)=>friend.id===friendId);
    identifiedFriend.isFavorite = !identifiedFriend.isFavorite;
    },
    addContact(name, phone, email){
      // blue printing the friend with newFriendContact
    let newFriendContact = {
      id: new Date().toISOString(),
      name: name,
      phone: phone,
      email: email,
      isFavorite: false
    };
    // adding our newly created blueprint/Friend above wth psh to th array
    this.friends.push(newFriendContact)
   },
   deleteContact(friendId){
    //overwriting the array info, instead of popping the friend off the friends array by filtering
    this.friends = this.friends.filter((friend) => friend.id !== friendId)
    // by filtering we are looking for inequality, if is equal we remove the item in the array
   }
   
   }
  
}
</script>
<style>
 *{
  box-sizing: border-box;
}

html {
  font-family: 'Jost', sans-serif;
}

body {
  margin: 0;
}

header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 3rem auto;
  border-radius: 10px;
  padding: 1rem;
  background-color: #58004d;
  color: white;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

#app li,
#app form {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  margin: 1rem auto;
  border-radius: 10px;
  padding: 1rem;
  text-align: center;
  width: 90%;
  max-width: 40rem;
}

#app h2 {
  font-size: 2rem;
  border-bottom: 4px solid #ccc;
  color: #58004d;
  margin: 0 0 1rem 0;
  text-align: center;
}

#app button {
  margin: .5rem;
  border-radius: 2px 2px;
  font: inherit;
  cursor: pointer;
  border: 1px solid rgba(0, 0, 0,.8);;
  background-color: #ff0077;
  color: white;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 2px rgba(0, 0, 0, 0.26);
}

#app button:hover,
#app button:active {
 
  background-color: #ec3169;
  border-color: #ec3169;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
}
/* style for the form */

#app input {
  font: inherit;
  padding: 0.15rem;
}
#app label {
  font-weight: bold;
  margin-right: 1rem;
  width: 7rem;
  display: inline-block;
}
#app form div {
  margin: 1rem 0;
}
</style>
