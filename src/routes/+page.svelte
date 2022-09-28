<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  const { url, param } = $page;

  let token = "Click Get Token";
  if (url.searchParams.get("code") !== null) {
    token = url.searchParams.get("code");
    console.log("token: " + token);
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

  const getOrders = async (token) => {
    console.log("getOrders token: " + token);
    //let getOrdersUrl = apiBasedUrl + "/ebay/getOrders/?code=" + token;
    let getOrdersUrl = apiBasedUrl + "/ebay/" + token + "/getOrders/";
    console.log("getOrdersUrl: " + getOrdersUrl);

    const res = await fetch(getOrdersUrl);
    orders = await res.json();
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<h1>token:{token}</h1>

<button on:click={getOrders(token)}> Get Orders </button>

<h1>orders:{orders}</h1>
