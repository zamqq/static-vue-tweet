<template>
  <div class="tweet-body">
    <div class="tweet-body-text">
      <span class="tweet-text">{{ parseTweetText }}</span>
      <div
        :class="{
          [`tweet-body-wrapper--${media.length}`]: media.length > 0,
        }"
        class="tweet-body-wrapper"
      >
        <div class="tweet-photos" v-for="item in media">
          <a
            v-if="item.type === 'photo'"
            :href="`https://twitter.com/${user.screen_name}/status/${idStr}`"
          >
            <img :src="item.media_url_https" alt="Main image" />
          </a>
          <video
            v-else-if="
              item.type === 'video' &&
              loadVideo &&
              item.video_info.variants[3].url
            "
            :src="item.video_info.variants[3].url"
            :type="item.video_info.variants[3].content_type"
            autoplay="autoplay"
            controls
          />
          <div v-else class="tweet-media--not-loaded">
            <img :src="item.media_url_https" alt="Fallback media URL" />
            <button @click="loadVideo = true">
              <svg viewBox="0 0 24 24" aria-hidden="true">
                <g><path d="M21 12L4 2v20l17-10z"></path></g>
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
    <div class="tweet-body-info">
      <a
        :href="`https://twitter.com/${user.screen_name}/status/${idStr}`"
        class="tweet-time"
      >
        <time datetime="">{{ parseTweetDate }}</time>
      </a>
      <a
        class="tweet-info-infolink"
        href="https://help.twitter.com/en/twitter-for-websites-ads-info-and-privacy"
        target="_blank"
        rel="noopener noreferrer"
      >
        <svg
          viewBox="0 0 24 24"
          aria-hidden="true"
          class="tweet-info_infoIcon__4u3D_"
        >
          <g>
            <path
              d="M13.5 8.5c0 .83-.67 1.5-1.5 1.5s-1.5-.67-1.5-1.5S11.17 7 12 7s1.5.67 1.5 1.5zM13 17v-5h-2v5h2zm-1 5.25c5.66 0 10.25-4.59 10.25-10.25S17.66 1.75 12 1.75 1.75 6.34 1.75 12 6.34 22.25 12 22.25zM20.25 12c0 4.56-3.69 8.25-8.25 8.25S3.75 16.56 3.75 12 7.44 3.75 12 3.75s8.25 3.69 8.25 8.25z"
            ></path>
          </g>
        </svg>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loadVideo: false,
    };
  },
  props: {
    media: {
      type: Object,
      default: () => {},
    },
    user: {
      type: Object,
      default: () => {},
    },
    idStr: {
      type: String,
      default: "",
    },
    data: {
      type: Object,
      default: () => {},
    },
  },
  computed: {
    parseTweetText() {
      const text = this.data.text;
      const newText = text.replace(/https?:\/\/[^\s]+/gim, "");
      return newText;
    },
    parseTweetDate() {
      const datetime = this.data.created_at;
      const a = new Date(datetime);
      const time = a.toLocaleString("en-US", {
        hour: "numeric",
        minute: "numeric",
        hour12: true,
      });
      const date = a.toLocaleString("en-US", {
        month: "short",
        day: "numeric",
        year: "numeric",
      });
      return time + " · " + date;
    },
  },
};
</script>

<style lang="scss">
.tweet-body {
  .tweet-body-text {
    font-size: 1.25rem;
    line-height: 1.5rem;
    overflow-wrap: break-word;
    white-space: pre-wrap;
    font-weight: 400;
    color: var(--tweet-font-color);
    a {
      color: var(--tweet-color-blue-secondary);
      text-decoration: none;
      &:hover {
        text-decoration: underline;
      }
    }

    .tweet-body-wrapper--1 {
      grid-template-columns: repeat(1, minmax(0, 1fr));
      height: 100%;
      .tweet-photos {
        max-height: 100%;
      }
    }

    .tweet-body-wrapper--2 {
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .tweet-body-wrapper--3 {
      grid-template-rows: repeat(2, minmax(0, 1fr));
      grid-template-columns: repeat(2, minmax(0, 1fr));

      .tweet-photos:first-child {
        grid-row: span 2 / span 2;
      }
    }

    .tweet-body-wrapper--4 {
      grid-template-rows: repeat(2, minmax(0, 1fr));
      grid-template-columns: repeat(2, minmax(0, 1fr));
    }

    .tweet-body-wrapper {
      display: grid;
      overflow: hidden;
      border: var(--tweet-border);
      border-radius: 0.75rem;
      margin-top: 0.75rem;
      grid-gap: 0.125rem;
      // height: 18.125rem;

      .tweet-photos {
        max-height: 18.125rem;
        max-width: 32.125rem;
        display: block;

        img {
          width: 100%;
          height: 100%;
          object-fit: cover;
        }

        video {
          height: 100%;
          width: 100%;
          object-fit: cover;
        }

        .tweet-media--not-loaded {
          width: 100%;
          height: 100%;
          display: flex;
          justify-content: center;
          align-items: center;
          position: relative;

          button {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            height: 4.188rem;
            width: 4.188rem;
            display: flex;
            align-items: center;
            justify-content: center;
            background-color: var(--tweet-color-blue-primary);
            transition-property: background-color;
            transition-duration: 0.2s;
            border: 4px solid #fff;
            border-radius: 50%;
            cursor: pointer;

            svg {
              margin-left: 0.25rem;
              width: calc(50% + 0.25rem);
              height: calc(50% + 0.25rem);
              max-width: 100%;
              color: #fff;
              fill: currentColor;
              -webkit-user-select: none;
              -moz-user-select: none;
              user-select: none;
            }
          }
        }
      }
    }
  }
  .tweet-body-info {
    margin-top: 0.75rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    .tweet-time {
      color: var(--tweet-font-color-secondary);
    }
    .tweet-info-infolink {
      width: 2rem;
      height: 2rem;
      border-radius: 50%;
      transition-duration: 0.2s;
      display: flex;
      justify-content: center;
      align-items: center;
      &:hover {
        background-color: var(--tweet-color-blue-secondary-hover);
        fill: var(--tweet-color-blue-primary);
      }
      svg {
        width: 1.25rem;
        height: 1.25rem;
      }
    }
  }
}
</style>
