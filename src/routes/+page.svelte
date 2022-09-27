<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  const { url, param } = $page;

  let code = "Click Get Access Token";
  if (url.searchParams.get("code") !== null) {
    code = url.searchParams.get("code");
    console.log("code: " + code);
  }

  const apiBasedUrl = "https://ebay-backend-django.herokuapp.com";
  let data = "";
  let orders = "Click Grab Order";

  /*
  onMount(async () => {
    code = await url.searchParams.get("code");
  });
  */

  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });

  const getOrders = async (code) => {
    console.log("getOrders code: " + code);
    let getOrdersUrl = apiBasedUrl + "/ebay/" + code + "/getOrders/";
    console.log("getOrdersUrl: " + getOrdersUrl);

    const res = await fetch(getOrdersUrl);
    orders = await res.json();
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<h1>code:{code}</h1>

<button on:click={getOrders(code)}> Get Orders </button>

<h1>orders:{orders}</h1>
