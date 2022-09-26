<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  const { url, param } = $page;
  const code = url.searchParams.get("code");

  const apiBasedUrl = "https://ebay-backend-django.herokuapp.com";
  let data = "";

  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });

  const getOrders = async (code) => {
    const res = await fetch(apiBasedUrl + "/ebay/getUser/" + code);
    data = await res.json();
  };
</script>

<h1>Access_token:{code}</h1>

<h1>Clicky the linky ;)</h1>
<h1>{data.signin_url}</h1>
<button
  class="btn waves-effect waves-light btn-large"
  type="submit"
  name="action"
  onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<button
  class="btn waves-effect waves-light btn-large"
  type="submit"
  name="action"
  onclick={data.signin_url}
  >Get Orders
</button>

<h1>orders:{orders}</h1>
