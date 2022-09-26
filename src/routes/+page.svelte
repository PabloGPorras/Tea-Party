<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";

  const { url, param } = $page;
  const code = url.searchParams.get("code").json();

  const apiBasedUrl = "https://ebay-backend-django.herokuapp.com";
  let data = "";
  let orders = "";
  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });

  const getOrders = async (code) => {
    const res = await fetch(apiBasedUrl + `/ebay/${code}/getOrders/`);
    orders = await res.json();
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<h1>Access_token:{code}</h1>

<button on:click={getOrders(code)}> Get Orders </button>

<h1>orders:{orders}</h1>
