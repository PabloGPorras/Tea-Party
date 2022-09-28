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
  let userData = "Click Get User Data";
  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });

  const getOrders = async (token) => {
    let getOrdersUrl = apiBasedUrl + "/ebay/" + token + "/30/getOrders/";
    const res = await fetch(getOrdersUrl);
    orders = await res.json();
    orders = orders.orders;
  };

  const getUsers = async (token) => {
    let getOrdersUrl = apiBasedUrl + "/ebay/" + token + "/getUser/";
    const res = await fetch(getOrdersUrl);
    userData = await res.json();
    console.log(userData);
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>
<h1>token:{token}</h1>

<button on:click={getOrders(token)}> Get Orders </button>
<h1>orders:{orders}</h1>

<button on:click={getUsers(token)}> Get User Data </button>
<h1>orders:{userData}</h1>
