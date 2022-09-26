<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  const { url, param } = $page;

  let access_token = "Click Get Access Token";
  let expires_in = "Click Get Access Token";
  let refresh_token = "Click Get Access Token";
  let refresh_token_expire_in = "Click Get Access Token";
  if (url.searchParams.get("accessToken") !== null) {
    access_token = url.searchParams.get("accessToken");
    expires_in = url.searchParams.get("expiresIn");
    refresh_token = url.searchParams.get("refreshToken");
    refresh_token_expire_in = url.searchParams.get("refreshTokenExpireIn");
  }

  const apiBasedUrl = "https://ebay-backend-django.herokuapp.com";
  let data = "";
  let orders = "Click Grab Order";
  onMount(async () => {
    const res = await fetch(apiBasedUrl + "/ebay/");
    data = await res.json();
  });

  const getOrders = async (access_token) => {
    const res = await fetch(apiBasedUrl + `/ebay/${access_token}/getOrders/`);
    orders = await res.json();
  };
</script>

<h1>{data.signin_url}</h1>
<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Get User Access Token
</button>

<h1>Access_token:{access_token}</h1>
<h1>expires_in:{expires_in}</h1>
<h1>refresh_token:{refresh_token}</h1>
<h1>refresh_token_expire_in:{refresh_token_expire_in}</h1>

<button on:click={getOrders(access_token)}> Get Orders </button>

<h1>orders:{orders}</h1>
