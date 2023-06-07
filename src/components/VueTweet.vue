<template>
  <div class="wrapper">
    <article class="embedded-tweet-article" v-if="tweet">
      <tweet-header :user="tweet.data.user" />
      <tweet-body
        :media="tweet.data.mediaDetails"
        :user="tweet.data.user"
        :id-str="tweet.data.id_str"
        :data="tweet.data"
      />
      <tweet-actions :data="tweet.data" />
      <tweet-replies :data="tweet.data" />
    </article>
    <article v-else>
      <tweet-skeleton />
    </article>
  </div>
</template>

<script>
import TweetHeader from "./TweetHeader.vue";
import TweetBody from "./TweetBody.vue";
import TweetActions from "./TweetActions.vue";
import TweetReplies from "./TweetReplies.vue";
import TweetSkeleton from "./TweetSkeleton.vue";

export default {
  name: "Tweet",
  data() {
    return {
      tweet: null,
    };
  },
  props: {
    id: {
      type: Number,
      required: true,
    },
    data: {
      type: Object,
      required: true,
    },
  },
  methods: {
    getTweet() {
      fetch(`https://react-tweet.vercel.app/api/tweet/${this.id}`)
        .then((response) => response.json())
        .then((data) => (this.tweet = data));
    },
  },
  components: {
    TweetHeader,
    TweetBody,
    TweetActions,
    TweetReplies,
    TweetSkeleton,
  },
  mounted() {
    this.getTweet();
  },
};
</script>

<style lang="scss">
.wrapper {
  display: flex;
  justify-content: center;
  padding: 2rem;
}
button {
  font-size: 0.9375em;
  background: none;
  border: none;
}
a {
  text-decoration: none;
  &:hover {
    text-decoration: underline;
  }
}
li {
  list-style: none;
}
.embedded-tweet-article {
  width: 34.25rem;
  font-family: var(--tweet-font-family);
  border: var(--tweet-border);
  border-radius: 12px;
  padding: 0.75rem 1rem 0.25rem;
  transition-property: background-color, box-shadow;
  transition-duration: 0.2s;
  background-color: var(--tweet-bg-color);
  &:hover {
    background-color: var(--tweet-bg-color-hover);
  }
}
</style>
