<template>
  <main>
  <ul class="o-vertical-spacing o-vertical-spacing--l">
    <li class="blog-post o-media">
      <div class="o-media__body">
        <div class="o-vertical-spacing">
          <h3 class="blog-post__headline">
            <span class="skeleton-box" style="width:3rem;height:3rem;border-radius:30%;margin-right: 1rem;"></span>
            <span class="skeleton-box" style="width:87%;height:3rem;"></span>
          </h3>
          <p>
            <span class="skeleton-box" style="width:100%;height:9.25rem;"></span>
            <hr style="border-color: var(--tweet-bg-color-hover);">
            <span class="skeleton-box" style="width:100%;height:2.25rem"></span>
            <span class="skeleton-box" style="width:100%;height:2.25rem;border-radius: 12px;"></span>
          </p>
        </div>
      </div>
    </li>
  </ul>
</main>
</template>

<style lang="scss">
ul {
  list-style: none;
  padding: 0;
  margin: 0;
  li {
    padding: 0;
    margin: 0;
  }
}
.skeleton-box {
  display: inline-block;
  height: 1em;
  position: relative;
  overflow: hidden;
  background-color: #eaeaea;
  border-radius: 4px;

  &::after {
    position: absolute;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    transform: translateX(-100%);
    background-image: linear-gradient(
      90deg,
      rgba(#fff, 0) 0,
      rgba(#fff, 0.2) 20%,
      rgba(#fff, 0.5) 60%,
      rgba(#fff, 0)
    );
    animation: shimmer 2s infinite;
    content: '';
  }

  @keyframes shimmer {
    100% {
      transform: translateX(100%);
    }
  }
}

.blog-post {
  &__headline {
    font-size: 1.25em;
    font-weight: bold;
  }

  &__meta {
    font-size: 0.85em;
    color: #6b6b6b;
  }
}

// OBJECTS

.o-media {
  display: flex;
  
  &__body {
    flex-grow: 1;
    padding: 0.25rem;
  }
}

.o-vertical-spacing {
  > * + * {
    margin-top: 0.75em;
  }
  
  &--l {
    > * + * {
      margin-top: 2em;
    }
  }
}

// MISC
main {
  width: 34.25rem;
  font-family: var(--tweet-font-family);
  border: var(--tweet-border);
  border-radius: 12px;
  padding: 0.75rem 1rem 0.25rem;
}

header {
  h1 {
    font-family: 'Rubik', sans-serif;
    font-weight: 500;
    line-height: 1.2;
    font-size: 2em;
  }

  p {
    &:not(:first-child) {
      margin-top: 1em;
    }
  }
}
</style>
