<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  const { url, param } = $page;
  const code = url.searchParams.get("access_token");

  const apiBasedUrl = "https://ebay-backend-django.herokuapp.com";
  let data = "";

  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });
</script>

<h1>{code}</h1>

<h1>Clicky the linky ;)</h1>
<h1>{data.signin_url}</h1>
<button
  class="btn waves-effect waves-light btn-large"
  type="submit"
  name="action"
  onclick="window.location.href = '{data.signin_url}';"
  >Submit
</button>
