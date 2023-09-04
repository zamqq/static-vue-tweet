<template>
  <div class="tweet-header">
    <a
      :href="`https://twitter.com/${user.screen_name}`"
      class="tweet-header-avatar"
    >
      <img :src="user.profile_image_url_https" width="48" height="48" alt="" />
    </a>

    <div class="tweet-header-author">
      <div class="tweet-header-author-linktext">
        <a :href="`https://twitter.com/${user.screen_name}`">
          <span>{{ user.name }}</span>
        </a>
        <svg
          v-if="user.is_blue_verified == true"
          :style="{ fill: fillColor }"
          viewBox="0 0 24 24"
          aria-label="Verified account"
          role="img"
          class="tweet-header_authorVerifiedIcon"
        >
          <g>
            <path
              d="M22.25 12c0-1.43-.88-2.67-2.19-3.34.46-1.39.2-2.9-.81-3.91s-2.52-1.27-3.91-.81c-.66-1.31-1.91-2.19-3.34-2.19s-2.67.88-3.33 2.19c-1.4-.46-2.91-.2-3.92.81s-1.26 2.52-.8 3.91c-1.31.67-2.2 1.91-2.2 3.34s.89 2.67 2.2 3.34c-.46 1.39-.21 2.9.8 3.91s2.52 1.26 3.91.81c.67 1.31 1.91 2.19 3.34 2.19s2.68-.88 3.34-2.19c1.39.45 2.9.2 3.91-.81s1.27-2.52.81-3.91c1.31-.67 2.19-1.91 2.19-3.34zm-11.71 4.2L6.8 12.46l1.41-1.42 2.26 2.26 4.8-5.23 1.47 1.36-6.2 6.77z"
            ></path>
          </g>
        </svg>
      </div>

      <div class="tweet-author-meta">
        <div class="tweet-author-tag">
          <a
            :href="`https://twitter.com/${user.screen_name}`"
            class="tweet-author-username"
          >
            <span> @{{ user.screen_name }} </span>
          </a>
        </div>
        <div class="tweet-header-authorfollow">
          <span class="spearator">·</span>
          <a
            :href="`https://twitter.com/intent/follow?screen_name=${user.screen_name}`"
            >Follow</a
          >
        </div>
      </div>
    </div>

    <a
      :href="`https://twitter.com/${user.screen_name}`"
      class="tweet-header-brand"
      rel="noopener noreferrer"
      aria-label="View on Twitter"
    >
      <svg
        viewBox="0 0 24 24"
        aria-hidden="true"
        class="tweet-header-twitter-icon"
      >
        <g>
          <path d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"></path>
        </g>
      </svg>
    </a>
  </div>
</template>

<script>
export default {
  name: "TweetHeader",
  props: {
    user: Object,
    required: true,
  },
  computed: {
    fillColor() {
      switch (this.user.verified_type) {
        case "Business":
          return "var(--tweet-verified-gold-color)";
        case "Government":
          return "var(--tweet-verified-gray-color)";
        default:
          return "var(--tweet-verified-blue-color)";
      }
    },
  },
};
</script>

<style lang="scss">
.tweet-header {
  display: flex;
  flex-direction: row;
  line-height: 1.25rem;
  align-items: stretch;
  padding-bottom: 0.75rem;
  .tweet-header-avatar {
    width: 3rem;
    height: 3rem;
    img {
      border-radius: 50%;
      transition-duration: 0.2s;
      &:hover {
        filter: brightness(85%);
      }
    }
  }
  .tweet-header-author {
    margin: 0 0.25rem;
    display: flex;
    flex-direction: column;
    justify-content: center;
    flex-grow: 2;
    .tweet-header-author-linktext {
      display: flex;
      flex-direction: row;
      align-items: center;
      span {
        color: var(--tweet-font-color);
        font-weight: 700;
      }
      svg {
        width: 1.172rem;
        height: 1.172rem;
        margin-left: 0.125rem;
      }
    }
    .tweet-author-meta {
      display: inline-flex;
      a {
        color: var(--tweet-font-color-secondary);
      }
      .tweet-author-username {
        text-decoration: none;
      }
      .tweet-header-authorfollow {
        a {
          font-weight: 700;
          color: var(--tweet-color-blue-secondary);
        }
        span {
          padding: 0 0.25rem;
        }
      }
    }
  }
  .tweet-header-brand {
    height: 100%;
    display: flex;
    justify-content: end;
    align-items: flex-start;
    .tweet-header-twitter-icon {
      width: 1.563rem;
      height: 1.563rem;
      fill: #000;
    }
  }
}
</style>
