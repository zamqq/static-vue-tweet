<template>
  <div class="tweet-actions">
    <a
      class="tweet-actions-like"
      :href="`https://twitter.com/intent/like?tweet_id=${data.id_str}`"
      rel="noopener noreferrer"
      aria-label="Like. This Tweet has 0 likes"
    >
      <div class="tweet-actions-like-icon-wrapper">
        <svg
          viewBox="0 0 24 24"
          class="tweet-actions_likeIcon"
          aria-hidden="true"
        >
          <g>
            <path
              d="M20.884 13.19c-1.351 2.48-4.001 5.12-8.379 7.67l-.503.3-.504-.3c-4.379-2.55-7.029-5.19-8.382-7.67-1.36-2.5-1.41-4.86-.514-6.67.887-1.79 2.647-2.91 4.601-3.01 1.651-.09 3.368.56 4.798 2.01 1.429-1.45 3.146-2.1 4.796-2.01 1.954.1 3.714 1.22 4.601 3.01.896 1.81.846 4.17-.514 6.67z"
            ></path>
          </g>
        </svg>
      </div>
      <span class="tweet-actions-like-count">{{
        nFormatter(data.favorite_count, 1)
      }}</span>
    </a>
    <a
      class="tweet-actions-reply"
      :href="`https://twitter.com/intent/tweet?in_reply_to=${data.id_str}`"
      rel="noopener noreferrer"
      aria-label="Reply to this Tweet on Twitter"
    >
      <div class="tweet-actions-reply-icon-wrapper">
        <svg
          viewBox="0 0 24 24"
          class="tweet-actions-replyIcon"
          aria-hidden="true"
        >
          <g>
            <path
              d="M1.751 10c0-4.42 3.584-8 8.005-8h4.366c4.49 0 8.129 3.64 8.129 8.13 0 2.96-1.607 5.68-4.196 7.11l-8.054 4.46v-3.69h-.067c-4.49.1-8.183-3.51-8.183-8.01z"
            ></path>
          </g>
        </svg>
      </div>
      <span class="tweet-actions-reply-text">Reply</span>
    </a>
    <button
      v-if="copiedLink"
      @click="copiedLink = false"
      type="button"
      class="tweet-actions-copy"
      aria-label="Copy link"
    >
      <div class="tweet-actions-copy-icon-wrapper">
        <svg
          viewBox="0 0 24 24"
          class="tweet-actions-copyIcon"
          aria-hidden="true"
        >
          <g>
            <path
              d="M9.64 18.952l-5.55-4.861 1.317-1.504 3.951 3.459 8.459-10.948L19.4 6.32 9.64 18.952z"
            ></path>
          </g>
        </svg>
      </div>
      <span class="tweet-actions-copyText"> Copied! </span>
    </button>
    <button
      v-else
      @click="
        copyURL(
          `https://twitter.com/${data.user.screen_name}/status/${data.id_str}`
        );
        returnCopyBtn();
        copiedLink = true;
      "
      type="button"
      class="tweet-actions-copy"
      aria-label="Copy link"
    >
      <div class="tweet-actions-copy-icon-wrapper">
        <svg
          viewBox="0 0 24 24"
          class="tweet-actions-copyIcon"
          aria-hidden="true"
        >
          <g>
            <path
              d="M18.36 5.64c-1.95-1.96-5.11-1.96-7.07 0L9.88 7.05 8.46 5.64l1.42-1.42c2.73-2.73 7.16-2.73 9.9 0 2.73 2.74 2.73 7.17 0 9.9l-1.42 1.42-1.41-1.42 1.41-1.41c1.96-1.96 1.96-5.12 0-7.07zm-2.12 3.53l-7.07 7.07-1.41-1.41 7.07-7.07 1.41 1.41zm-12.02.71l1.42-1.42 1.41 1.42-1.41 1.41c-1.96 1.96-1.96 5.12 0 7.07 1.95 1.96 5.11 1.96 7.07 0l1.41-1.41 1.42 1.41-1.42 1.42c-2.73 2.73-7.16 2.73-9.9 0-2.73-2.74-2.73-7.17 0-9.9z"
            ></path>
          </g>
        </svg>
      </div>
      <span class="tweet-actions-copyText"> Copy link</span>
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      copiedLink: false,
    };
  },
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
  methods: {
    nFormatter(num, digits) {
      const lookup = [
        { value: 1, symbol: "" },
        { value: 1e3, symbol: "k" },
        { value: 1e6, symbol: "M" },
      ];
      const rx = /\.0+$|(\.[0-9]*[1-9])0+$/;
      var item = lookup
        .slice()
        .reverse()
        .find(function (item) {
          return num >= item.value;
        });
      return item
        ? (num / item.value).toFixed(digits).replace(rx, "$1") + item.symbol
        : "0";
    },
    async copyURL(mytext) {
      try {
        await navigator.clipboard.writeText(mytext);
      } catch ($e) {
        alert("Cannot copy");
      }
    },
    returnCopyBtn() {
      setTimeout(() => {
        this.copiedLink = false;
      }, 3000); // 3 seconds
    },
  },
};
</script>

<style lang="scss">
@mixin tweet-actions($color, $color-hover, $class-iconWrapper) {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-right: 1.25rem;
  color: var(--tweet-font-color-secondary);
  padding: 0;
  &:hover {
    color: var(--tweet-color-#{$color});
    fill: var(--tweet-color-#{$color});
    text-decoration: underline var(--tweet-color-#{$color});

    .#{$class-iconWrapper} {
      background-color: var(--tweet-color-#{$color-hover});
    }
  }
  span {
    font-weight: 700;
    margin-left: 0.267rem;
  }
  .#{$class-iconWrapper} {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    svg {
      width: 1.25rem;
      height: 1.25rem;
      fill: var(--tweet-color-#{$color});
    }
  }
}

.tweet-actions {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  border-top: var(--tweet-border);
  margin-top: 0.25rem;
  padding-top: 0.25rem;
  .tweet-actions-like {
    @include tweet-actions(
      red-primary,
      red-primary-hover,
      tweet-actions-like-icon-wrapper
    );
  }
  .tweet-actions-reply {
    @include tweet-actions(
      blue-primary,
      blue-secondary-hover,
      tweet-actions-reply-icon-wrapper
    );
  }
  .tweet-actions-copy {
    @include tweet-actions(
      green-primary,
      green-primary-hover,
      tweet-actions-copy-icon-wrapper
    );
  }
}
</style>
