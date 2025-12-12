<script>
  import { loadStripe } from "@stripe/stripe-js";
  import { PUBLIC_STRIPE_KEY } from '$env/static/public'
  import { redirect } from '@sveltejs/kit';

  let { children, ...props } = $props()

  async function onclick() {
    const stripe = await loadStripe(PUBLIC_STRIPE_KEY)

    const response = await fetch("/api/checkout", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        }
    })

    const {session} = await response.json();
    window.location.href = session.url;
  }
</script>


<style>
  button {
    background-color: black;
    color: white;
    padding: 20px 24px;
    font-weight: normal;
    font-size: 22px;
    text-transform: uppercase;
    transition: all 0.3s;
    border: 1px solid white;
  }

  button:hover {
    background-color: white;
    color: black;
  }
</style>



<button {...props} {onclick}>
  {@render children() }
</button>


