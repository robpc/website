<script lang="ts">
  import type { Pricing } from "$lib/types/pricing.type";
  import QaTooltip from "../qa-tooltip.svelte";

  export let pricing: Pricing;
  const {
    title,
    duration,
    features,
    price,
    btnHref,
    btnText,
    spiced,
    learnMoreHref,
    footnote,
    trackingName,
  } = pricing;
</script>

<style lang="postcss">
  .box {
    width: 295px;

    @media (max-width: 375px) {
      @apply w-full;
    }
  }

  .h1 {
    margin-bottom: 0.25rem;
  }

  li::before {
    content: url("/tick.svg");
    @apply absolute inline-block -left-7 sm:-left-9;
    height: 1.375rem;
    width: 1.375rem;

    @media (max-width: 375px) {
      @apply h-5 w-5;
    }
  }

  .btn-cta {
    @apply self-center;
  }

  .learn-more {
    @apply underline;
  }

  :global(.crossed-out) {
    @apply line-through;
  }

  :global(.price-small),
  :global(.crossed-out) {
    @apply text-gray-800 text-h4 mr-macro;
  }
</style>

<div
  class={`box flex flex-col justify-between bg-gray-100 pt-x-small pb-medium px-0 mt-0 mx-micro mb-x-small rounded-2xl shadow-normal text-center transition-all duration-200 hover:shadow-brand ${
    spiced ? "spiced shadow-brand" : ""
  }`}
>
  <div class="min-h-full flex flex-col">
    <h2 class="h4">{title}</h2>
    <div class="h1 font-bold text-black flex items-center justify-center">
      {@html price}
    </div>
    <div class="mb-xx-small text-dark-grey font-semibold">
      {#if duration}
        {duration}
      {:else}
        <span>&nbsp;</span>
      {/if}
    </div>
    {#if features}
      <ul
        class="mx-small sm:mx-medium lgx:mx-small my-small space-y-micro text-left"
      >
        {#each features as feature}
          <li class="relative flex text-black">
            {#if typeof feature !== "string"}
              <QaTooltip text={feature.text} tooltip={feature.tooltip} />
            {:else}
              {feature}
            {/if}
          </li>
        {/each}
      </ul>
    {/if}
    {#if learnMoreHref}
      <div class="flex flex-1 justify-center items-center">
        <a href={learnMoreHref} class="learn-more">Learn More</a>
      </div>
    {/if}
  </div>
  {#if btnHref && btnText}
    <a
      href={btnHref}
      data-analytics={`{"context":"` + trackingName + `","position":"hero"}`}
      class="btn-cta"
      class:btn-primary={spiced}>{btnText}</a
    >
  {/if}
  {#if footnote}
    <div class="text-p-xsmall px-small text-gray-800">{footnote}</div>
  {/if}
</div>
