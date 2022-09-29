<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  const { url, param } = $page;

  let UserID = "";
  let Email = "";
  let FeedbackScore = "";
  let visible = true;

  if (url.searchParams.get("sellerInfo") !== null) {
    data = url.searchParams.get("sellerInfo");
    sellerInfo = data.json();
    UserID = sellerInfo.UserID;
    Email = sellerInfo.Email;
    FeedbackScore = "FeedbackScore: " + sellerInfo.FeedbackScore;
    visible = !visible;
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
    data = await res.json();
    orders = data.getOrders;
  };

  const getUser = async (token) => {
    let getOrdersUrl = apiBasedUrl + "/ebay/" + token + "/getUser/";
    const res = await fetch(getOrdersUrl);
    data = await res.json();
    userData = data.getUser;
  };
</script>

<h1>{UserID}</h1>
<h1>{Email}</h1>
<h1>{FeedbackScore}</h1>

{#if visible}
  <button type="submit" onclick="window.location.href = '{data.signin_url}';"
    >Login
  </button>
{/if}
