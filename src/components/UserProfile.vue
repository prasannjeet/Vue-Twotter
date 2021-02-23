<template>
  <div className="user-profile">
    <div className="user-profile__user-panel">
      <h1 className="user-profile__username">@{{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="this.user.isAdmin">Admin</div>
      <div class="user-profile__admin-badge" v-else>User</div>
      <div className="user-profile__follower_count">
        <strong>Followers: </strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile__twoots-wrapper">
      <TwootItem v-for="twoot in this.user.twoots"
                 :key="twoot.id"
                 :username="this.user.username"
                 :twoot="twoot"
                 @favourite="toggleFavourite"
      />
    </div>
  </div>
</template>

<script lang="js">

import TwootItem from "@/components/TwootItem";

export default {
  name: 'user-profile',
  components: {TwootItem},
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: 'prasannjeet',
        firstName: 'Prasannjeet',
        lastName: 'Singh',
        email: 'prasannjeetsingh@gmail.com',
        isAdmin: true,
        twoots: [
          {
            id: 1,
            content: "Twotter is amazing!"
          },
          {
            id: 2,
            content: "Like my project? Clone it and work with it! "
          }
        ]
      }
    }
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower!`)
      }
    }
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.lastName}`
    }
  },
  methods: {
    followUser() {
      this.followers++
    },
    toggleFavourite(id) {
      console.log(`Favourited Tweet #${id}`)
    }
  },
  mounted() {
    this.followUser();
  }
}
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #DFE3E8;
}

.user-profile__admin-badge {
  background: rebeccapurple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}

h1 {
  margin: 0;
}
</style>
