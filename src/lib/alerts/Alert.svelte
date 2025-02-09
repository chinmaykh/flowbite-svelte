<script lang="ts">
  import classNames from 'classnames';
  import { createEventDispatcher, type ComponentProps } from 'svelte';
  import CloseButton from '../utils/CloseButton.svelte';
  import Frame from '../utils/Frame.svelte';

  export let dismissable: boolean = false;
  export let defaultClass: string = 'p-4 gap-3 text-sm';

  const dispatch = createEventDispatcher();

  interface $$Props extends ComponentProps<Frame> {
    dismissable?: boolean;
  }

  let hidden = false;

  const close = () => {
    hidden = !hidden;
    dispatch('close'); // preferred name
  };

  let divClass: string;
  $: divClass = classNames(
    defaultClass,
    ($$slots.icon || dismissable) && 'flex items-center',
    hidden && 'hidden',
    $$props.class
  );

  $: {
    // set default values
    $$restProps.color = $$restProps.color ?? 'primary';
    $$restProps.rounded = $$restProps.rounded ?? true;
  }
</script>

<Frame {...$$restProps} class={divClass} role="alert">
  {#if $$slots.icon}
    <slot name="icon" />
  {/if}

  {#if $$slots.icon || dismissable}
    <div><slot /></div>
  {:else}
    <slot />
  {/if}

  {#if dismissable}
    <slot name="close-button" {close}>
      <CloseButton
        class="'-mx-1.5 -my-1.5'"
        color={$$restProps.color}
        on:click={close}
        on:click
        on:change
        on:keydown
        on:keyup
        on:focus
        on:blur
        on:mouseenter
        on:mouseleave />
    </slot>
  {/if}
</Frame>

<!--
  @component
  ## Features
  [Go to Alert](https://flowbite-svelte.com/docs/components/alert)
  - Default alert
  - Alerts with icon
  - Bordered alerts
  - Alerts with list
  - Dismissable alerts
  - Border accent
  - Additional content
  - Custom color
  ## Props
  @prop dismissable: boolean = false;
  @prop accent: boolean = false;
  ## Event
  - on:click
  - on:change
  - on:keydown
  - on:keyup
  - on:focus
  - on:blur
  - on:mouseenter
  - on:mouseleave 

  ## Example
  ```
  <script>
  import {Alert} from "flowbite-svelte";
  </script>

  <Alert>
    <span class="font-medium">Info alert!</span> Change a few things up and try submitting again.
  </Alert>
  <Alert color="red">
    <span class="font-medium">Danger alert!</span> Change a few things up and try submitting again.
  </Alert>
  ```
-->
