<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  let access_token = "Click Get Access Token";
  let code = "";
  const { url, param } = $page;
  if (url.searchParams.get("code") !== null) {
    code = url.searchParams.get("code");
    access_token = code.access_token;
  }

  const apiBasedUrl = "https://ebay-backend-django.herokuapp.com";
  let data = "";
  let orders = "Click Grab Order";
  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });

  const getOrders = async (code) => {
    const res = await fetch(
      apiBasedUrl + `/ebay/${code.access_token}/getOrders/`
    );
    orders = await res.json();
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<h1>Access_token:{access_token}</h1>

<button on:click={getOrders(code)}> Get Orders </button>

<h1>orders:{orders}</h1>
