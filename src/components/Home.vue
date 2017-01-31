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
        <div v-for="tweet in list" class="ui segment">
          <div class="ui feed">
            <div class="event">
              <div class="label">
                <img class="titleImage" v-if="tweet.user" :src="tweet.user.photo">
              </div>
              <div class="content">
                <div class="date">
                  {{ tweet.timestamp | fromNow }}
                </div>
                <div class="summary">
                  <a v-if="tweet.user">{{ tweet.user.name }}</a>
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
    users: {},
    checkUser: false
  }),
  created () {
    Tweet.list((list) => {
      this.tweets = list
    })
    User.list((list) => {
      this.users = list.reduce((p, v) => {
        p[v.$id] = v
        return p
      }, {})
    })
    this.checkUser = Auth.getCurrentUser()
  },
  computed: {
    list () {
      return this.tweets.map((tweet) => {
        return {
          ...tweet,
          user: this.users[tweet.owner]
        }
      })
    }
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
    }
  }
}
</script>