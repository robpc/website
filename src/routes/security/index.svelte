<script context="module">
  export const prerender = true;
</script>

<script>
  import Secure from "$lib/components/security/secure.svelte";
  import Program from "$lib/components/security/program.svelte";
  import CallToAction from "$lib/components/security/call-to-action.svelte";
  import Report from "$lib/components/security/report.svelte";
  import OpenGraph from "$lib/components/open-graph.svelte";
  import UsedBy from "$lib/components/index/used-by.svelte";
</script>

<OpenGraph
  data={{
    description: "Does Gitpod encrypt data?",
    title: "Security",
  }}
/>

<header class="tight">
  <h1>Security at Gitpod</h1>
  <p class="max-w-2xl mx-auto mb-x-small">
    Gitpod is trusted by over 500k developers and companies that are moving
    their dev environments to the cloud.
  </p>
  <a href="/contact/support" class="btn btn-primary">Talk to an expert</a>
</header>
<UsedBy
  title="Trusted by developer led companies"
  class="bg-off-white rounded-2xl shadow-normal pt-small pb-9"
/>
<Secure />
<Program />
<CallToAction />
<Report />
