<template>
  <div class="tweet-replies">
    <a
      class="tweet-replies-link"
      :href="`https://twitter.com/'${data.user.screen_name}/status/${data.id_str}`"
      target="_blank"
      rel="noopener noreferrer"
    >
      <span class="tweet-replies-text"
        >Read {{ data.conversation_count }} replies</span
      >
    </a>
  </div>
</template>
<script>
export default {
  props: {
    data: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style lang="scss">
.tweet-replies {
  display: flex;
  justify-content: center;
  padding: 0.25rem 0 0.75rem 0;
  .tweet-replies-link {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0 1rem;
    width: 100%;
    height: 2rem;
    border: var(--tweet-border);
    border-radius: 0.75rem;
    transition-duration: 0.2s;
    text-decoration: none;
    &:hover {
      background-color: var(--tweet-color-blue-secondary-hover);
    }
    span {
      font-weight: 700;
      color: var(--tweet-color-blue-secondary);
    }
  }
}
</style>
