<script lang="ts">
  import { faqsKey } from "./faqs.svelte";
  import { getContext, onMount } from "svelte";
  import { stringToBeautifiedFragment } from "$lib/utils/helpers";

  export let title: string;

  const activeFaq: any = getContext(faqsKey);
  const fragment = stringToBeautifiedFragment(title);

  const setActive = ({ target }) => {
    const open = target.open;
    if (open) {
      $activeFaq = title;
    }
    // closing the faq that was active, no faq will remain open
    if (isActive && !open) $activeFaq = null;
  };

  onMount(() => {
    isActive = fragment === window.location.hash.substring(1);
  });

  $: isActive = $activeFaq === title;
</script>

<style lang="scss">
  .faq {
    border-radius: 16px;
    background: var(--sand-dark);
    border: 1px solid transparent;

    &:hover,
    &:focus {
      border: 1px solid var(--white);
    }

    &:not(:last-child) {
      margin-bottom: var(--xx-small);
    }

    &__top {
      padding: var(--medium);
      align-items: center;

      @media (max-width: 860px) {
        padding: var(--xx-small);
        align-items: flex-start;
      }

      @media (max-width: 375px) {
        padding: var(--micro);
      }
    }

    &__title {
      display: inline-block;
      width: 86%;
    }

    &__arrow {
      height: 1.5rem;
      width: 1.5rem;
      outline: none;
      transition: all 0.2s;

      @media (max-width: 768px) {
        margin-top: 0.188rem;
      }
    }

    &__text {
      margin: var(--medium);
      margin-top: -2.5rem;

      @media (max-width: 860px) {
        margin: var(--xx-small);
        margin-top: -1rem;
      }

      @media (max-width: 375px) {
        margin: var(--micro);
        margin-top: -0.5rem;
      }
    }

    & :global(a) {
      font-weight: 600;
    }
  }

  .h4 {
    margin-bottom: 0;
  }

  details[open] .faq__arrow {
    transform: rotate(180deg);
  }

  summary {
    list-style: none;
  }

  summary::-webkit-details-marker {
    display: none;
  }
</style>

<details
  class="faq"
  open={isActive}
  on:toggle={setActive}
  id={fragment}
  data-analytics={`{"context":"faq"}`}
>
  <summary class="outline-none">
    <div class="faq__top flex">
      <h3 class="h4 faq__title flex-1">{title}</h3>
      <img
        class="faq__arrow ml-macro"
        width="24"
        height="24"
        src="/arrow.svg"
        alt="Arrow"
      />
    </div>
  </summary>
  <div class="faq__text text-large">
    <slot />
  </div>
</details>
