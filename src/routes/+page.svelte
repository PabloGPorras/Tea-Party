<script>
  import { onMount } from "svelte";
  import { page } from "$app/stores";
  const { url, param } = $page;

  let UserID = "";
  let Email = "";
  let FeedbackScore = "";

  if (url.searchParams.get("sellerInfo") !== null) {
    sellerInfo = url.searchParams.get("sellerInfo");
    console.log(sellerIfno);
    console.log("_______________________________");
    sellerInfo = JSON.parse(sellerInfo);
    console.log(sellerIfno);
    UserID = sellerInfo.UserID;
    Email = sellerInfo.Email;
    FeedbackScore = sellerInfo.FeedbackScore;
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
</script>

<h1>{UserID}</h1>
<h1>{Email}</h1>
<h1>{FeedbackScore}</h1>

<button type="submit" onclick="window.location.href = '{data.signin_url}';"
  >Login
</button>
