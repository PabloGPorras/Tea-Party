<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  const { url, param } = $page;

  let access_token = "Click Get Access Token";
  if (url.searchParams.get("access_token") !== null) {
    access_token = url.searchParams.get("access_token");
    console.log("access_token: " + access_token);
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

  const getOrders = async (access_token) => {
    console.log("getOrders access_token: " + access_token);
    let getOrdersUrl =
      apiBasedUrl + "/ebay/getOrders/?access_token=" + access_token;
    console.log("getOrdersUrl: " + getOrdersUrl);

    const res = await fetch(getOrdersUrl);
    orders = await res.json();
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<h1>access_token:{access_token}</h1>

<button on:click={getOrders(access_token)}> Get Orders </button>

<h1>orders:{orders}</h1>
