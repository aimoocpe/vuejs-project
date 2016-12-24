<template>
    <div class="ui basic segment">
        <div v-if="checkUser" class="ui segment">
            <form @submit.prevent="post" class="ui form">
                <div class="field">
                    <textarea v-model="input">
                </div>
                <button class="ui blue button" :class="{'loading disabled': posting}">Post</button>
            </form>
        </div>
        <div v-for="tweet in tweets" class="ui segment">
          <div class="ui feed">
            <div class="event">
              <div class="label">
                <img class="titleImage" v-if="findUserPhoto(tweet.owner)" :src="findUserPhoto(tweet.owner)">
              </div>
              <div class="content">
                <div class="date">
                  {{ tweet.timestamp | fromNow }}
                </div>
                <div class="summary">
                  <a>{{ findUserName(tweet.owner) }}</a>
                </div>
                <div class="extra text">
                  {{ tweet.content }}
                </div>
              </div>
            </div>
          </div>
        </div>
        
    </div>
</template>

<style scoped>
  .titleImage {
    height: 32px !important;
  }
</style>

<script>
import { Tweet, User, Auth } from '../services'

export default {
  data: () => ({
    input: '',
    posting: false,
    tweets: [],
    users: [],
    checkUser: false
  }),
  created () {
    Tweet.list((list) => {
      this.tweets = list
    })
    User.list((list) => {
      this.users = list
    })
    this.checkUser = Auth.getCurrentUser()
  },
  methods: {
    post () {
      if (!this.input) return
      this.posting = true
      Tweet.post(this.input)
        .then(() => {
          this.input = ''
          this.posting = false
        })
    },
    findUserName (id) {
      const x = this.users.find((it) => it.$id === id)
      return x ? x.name : ''
    },
    findUserPhoto (id) {
      const x = this.users.find((it) => it.$id === id)
      return x ? x.photo : ''
    }
  }
}
</script>