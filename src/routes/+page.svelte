<script lang="ts">
  import { BlurInView, FadeInView, FlyInView } from "$lib/index.js";
  import { quartIn } from "svelte/easing";
  let exampleArray: string[] = [
    "You",
    "can",
    "iterate",
    "over",
    "arrays",
    "with",
    "each",
    "🔥",
  ];
</script>

<div class="intro">
  <h1>Welcome to svelte-transition-inview</h1>
  <p>
    Reuse these transition components anywhere with custom options. Wrap them
    with styled elements to control position / sizing etc. You can use many
    instances, nested within others, and / or map over arrays of data.
  </p>
  <p>
    examples are wrapped in a div with height: 100vh; font-size: 22px; width:
    50%;
  </p>
</div>

<h1 class="heading">BLUR</h1>
<div class="wrapper">
  <BlurInView
    options={{
      delay: 1000,
      duration: 300,
      amount: 5,
      opacity: 0,
    }}
  >
    I'm delayed by 1 second, oh wait...
    <BlurInView
      options={{
        delay: 3000,
        duration: 300,
        amount: 5,
        easing: quartIn,
        opacity: 0,
      }}
    >
      <div style=" background-color: indianred; color: white;">
        I'm nested instance inside with a delay of 3 secs
      </div>
    </BlurInView>
  </BlurInView>

  <BlurInView
    options={{
      delay: 5000,
      duration: 300,
      amount: 5,
      easing: quartIn,
      opacity: 0,
    }}
  >
    <div style="margin-top: 100px;">
      I am at the level of the first in the dom, with margin top 100px, delayed
      by 5 secs
    </div>
  </BlurInView>
</div>

<h1 class="heading">FADE</h1>
<div class="wrapper">
  <div
    style="display: grid; grid-template-columns: repeat(auto-fit, 100px);grid-auto-flow: column;"
  >
    {#each exampleArray as el, i}
      <FadeInView options={{ delay: 250 * i }}>
        {el}
      </FadeInView>
    {/each}
  </div>
</div>

<style>
  .intro {
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
  }
  .wrapper {
    width: 50%;
    height: 100vh;
    font-size: 22px;
  }
  .heading {
    text-align: center;
    margin: 12px 12px 0 0;
    font-size: 42px;
  }
</style>
