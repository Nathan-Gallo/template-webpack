<script>
  import { createEventDispatcher } from 'svelte';

  export let book = {};

  const dispatch = createEventDispatcher();
  function isValidUrl(url) {
    return url && /http.+\.(jpg|png|gif)$/.test(url);
  }

  const handleClick = (id) => alert("clicked book" + id);
</script>

<a
  href="#"
  class="book book--interactive book--variation-{book.variation}
  {isValidUrl(
    book.cover
  )
    ? 'book--cover'
    : 'book--no-cover'}"
  on:click={() => dispatch('book-select', { id: book.id })}
>
  <span
    class="cover"
    style={isValidUrl(book.cover)
      ? "background-image: url(" + book.cover + ")"
      : ""}
  >
    <span class="title">{isValidUrl(book.cover) ? "" : book.title || ""}</span>
    <span class="author">{isValidUrl(book.cover) ? "" : book.author || ""}</span
    >
  </span>
</a>

<style>
  .book {
    --bg: #f5c839;
    --bgDark: #f3b131;
    --bgLight: #ffde77;

    background: #fff;
    border-radius: 4px;
    box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.25);
    position: relative;
    transition: all 550ms;
    width: 100%;
  }

  .book--variation-1 {
    --bg: #ea7025;
    --bgDark: #d7480b;
    --bgLight: #fb9c61;
  }
  .book--variation-2 {
    --bg: #76c267;
    --bgDark: #57b356;
    --bgLight: #a6e69a;
  }

  .book--interactive {
    border: none;
    cursor: pointer;
  }
  .book--interactive:hover,
  .book--interactive:focus {
    filter: brightness(90%);
    outline: none;
  }

  .cover,
  .title,
  .author {
    display: block;
  }
  .cover {
    background-image: linear-gradient(
      to right,
      var(--bgLight) 10%,
      var(--bg) 20%
    );
    background-size: cover;
    background-repeat: no-repeat;
    border-radius: 4px;
    color: #000;
    font-size: var(--typeSizeLarge);
    height: 100%;
    left: 0;
    overflow: hidden;
    position: absolute;
    text-align: left;
    text-transform: uppercase;
    text-shadow: 2px 2px 0 #fff;
    top: 0;
    transition: all 300ms;
    width: 100%;
  }
  .book--no-cover .cover::before {
    background: linear-gradient(to right, var(--bg) 50%, var(--bgDark));
    content: " ";
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    width: 10%;
  }
  .book--interactive:hover .cover,
  .book--interactive:focus .cover {
    box-shadow: 0.375rem 0.25rem 0.25rem rgba(0, 0, 0, 0.25);
    transform: translate(0.0625rem, -0.3125rem) skew(0, -5deg) scaleX(1.02);
  }
  .title {
    font-size: var(--typeSizeXLarge);
    font-weight: var(--typeWeightBold);
    line-height: var(--typeLineHeightTight);
    margin: 3rem 0 var(--spacingMedium) calc(10% + var(--spacingSmall));
  }
  .author {
    letter-spacing: 0.25em;
    margin-left: calc(10% + var(--spacingSmall));
  }
</style>
