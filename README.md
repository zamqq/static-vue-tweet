# static-vue-tweet

A statically-rendered tweet component using Vue 3, Scss, and Vercel's API.
This project wouldn't exist without https://static-tweet.vercel.app/.

## The problem

The official tweet embed provides you with a `<blockquote>` element containing the tweet text and a third-party script to replace it with an `<iframe>` containing a better UI.

This method of embedding tweets has some disadvantages:

- Initial page load does not display the tweets.
- The tweet widget JS loads after pageload.
- An iframe is initialized, kicking off more JS. The page content shifts around to make room.
- A whole webview is rendered inside the iframe. More page layout shift.

## The solution

A good solution would be to get the tweet data from the API then use plain HTML & CSS to display it, which gives you the best lighthouse scores.

## Install

```bash
npm install static-vue-tweet
```

## Quickstart

```javascript
import { VueTweet } from "static-vue-tweet";

<Tweet id="1656183755000762373" />;
```
