<script lang="ts">
  import type { NavbarType } from '../types';
  import { clickOutside } from '../utils/clickOutside';

  export let liButtonClass: string = 'flex items-center justify-between w-full';
  export let name: string;
  export let child: NavbarType[] = [];
  export let dropdownDiv: string = '';
  export let dropdownLinkClassWithChild: string | undefined = undefined;
  export let rel: string | undefined = undefined;

  let hidden = true;
  let block = false;

  const handleDropdown = () => {
    hidden = !hidden;
    block = !block;
  };

  let liClass =
    'flex justify-center py-2 pr-4 pl-3 text-gray-700 border-b border-gray-100 hover:bg-gray-50 md:hover:bg-transparent md:border-0 md:hover:text-primary-700 md:p-0 dark:text-gray-400 md:dark:hover:text-white dark:hover:bg-gray-700 dark:hover:text-white md:dark:hover:bg-transparent dark:border-gray-700';
</script>

<li use:clickOutside={() => !hidden && handleDropdown()} class={liClass}>
  <button on:click={() => handleDropdown()} class={liButtonClass}
    >{name}
    <svg class="ml-1 w-4 h-4" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"
      ><path
        fill-rule="evenodd"
        d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
        clip-rule="evenodd" /></svg
    ></button>

  <!-- Dropdown menu -->
  <div class:hidden class="absolute {dropdownDiv} mt-8 z-10">
    <slot>
      <ul class="py-1" aria-labelledby="dropdownLargeButton">
        {#each child as item}
          <li>
            <a
              href={item.href}
              {rel}
              on:blur
              on:change
              on:click
              on:focus
              on:keydown
              on:keypress
              on:keyup
              on:mouseenter
              on:mouseleave
              on:mouseover
              class={dropdownLinkClassWithChild}>{item.name}</a>
          </li>
        {/each}
      </ul>
    </slot>
  </div>
</li>

<!--
  @component
  [Go to Navbar](https://flowbite-svelte.com/docs/components/navbar)
  ## Props
  @prop liButtonClass: string = 'flex items-center justify-between w-full';
  @prop name: string;
  @prop child: NavbarType[] = [];
  @prop dropdownDiv: string = '';
  @prop dropdownLinkClassWithChild: string | undefined = undefined;
  @prop rel: string | undefined = undefined;
  ## Event
  - on:blur
  - on:change
  - on:click
  - on:focus
  - on:keydown
  - on:keypress
  - on:keyup
  - on:mouseenter
  - on:mouseleave
  - on:mouseover
  ## Example
  ```
  <script>
    import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte'
  </script>

  <Navbar let:hidden let:toggle>
    <NavBrand href="/">
      <img
        src="/images/flowbite-svelte-icon-logo.svg"
        class="mr-3 h-6 sm:h-9"
        alt="Flowbite Logo"
      />
      <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">
        Flowbite
      </span>
    </NavBrand>
    <NavHamburger on:click={toggle} />
    <NavUl {hidden}>
      <NavLi href="/" active={true}>Home</NavLi>
      <NavLi href="/about">About</NavLi>
      <NavLi href="/services">Services</NavLi>
      <NavLi href="/pricing">Pricing</NavLi>
      <NavLi href="/contact">Contact</NavLi>
    </NavUl>
  </Navbar>
  ```
-->
