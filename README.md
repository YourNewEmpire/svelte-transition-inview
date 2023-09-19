# svelte-transition-inview

Components for transitioning when entering the viewport. Components exported for blur, fade, fly, scale and slide transitions. The svg draw transition remains out there for someone to try in a PR or something

This is pretty much it so far: 

`import {BlurInView, FadeInView, FlyInView, ScaleInView, SlideInView} from "svelte-transition-inview"`

## Installing

```
pnpm create svelte@latest my-app

pnpm i svelte-transition-inview

```
or just as dev dependancy


```
pnpm i -d svelte-transition-inview

```


## Examples

```
<script>
import {BlurInView} from "svelte-transition-inview"
</script>

<div class="page">

  <BlurInView>
      I have default options
  </BlurInView>

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
      <div style=" background-color: indianred;">
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
      I am at the level of the first transition in the dom, with margin top 100px, delayed
      by 5 secs
    </div>
  </BlurInView>

</div>
```

Mapping over data? You can still do great things like manipulating delay in each iteration.

```
<script>
import {BlurInView} from "svelte-transition-inview"

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

<div class="page">

  <div
    style="display: grid; grid-template-columns: repeat(auto-fit, 100px); grid-auto-flow: column;"
  >
    {#each exampleArray as el, i}
      <FadeInView options={{ delay: 250 * i }}>
        {el}
      </FadeInView>
    {/each}
  </div>

</div>
```

By default, the component transitions in, but not out. Control how the component transitions out with the optional outOptions prop. `"off"` is default and will keep the element rendered after leaving the viewport. use `outOptions="static"` to repeat transition when re-entering the viewport. 


Lastly, you can pass your own out transition object: `outOptions={TransitionObj}` 

```
 // Possible args: FlyParams | "static" | "off"
 
  <FlyInView outOptions="static">
    content
  </FlyInView>
  ```