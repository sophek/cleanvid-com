<template>
  <div>
    <div class="p-grid" style="background-color:#ffffff;padding:5%">
      <div class="p-col-12 p-md-6 p-lg-6">
        <h2>Introducing CleanVid, the world’s first fully automated multiple platform video ad-skipping service.</h2>
        <br />
        <p class="paragraph">
          For $49.99 per year, you have the abliity to skips all the ads you want on over 15 ad supported streaming services.
          <br />
        </p>
        <p
          class="paragraph"
        >Comparing that to buying for one year of upgrades so you can skip ads, Youtube premium ($143.88), Hulu ads-free ($72.00), and CBS all access upgrade ($48.00). $263.88 in additional cost per year vs $49.99 with CleanVid. With CleanVid you can save $213.89 per year.</p>
        <br />
        <br />
        <stripe-checkout
          ref="checkoutYearlyRef"
          pk="pk_test_GOYwfBk7nZhol9yUB35Yr469"
          :items="items"
          :successUrl="successUrl"
          :cancelUrl="cancelUrl"
        >
          <template slot="checkout-button">
            <Button
              @click="checkout"
              style="background-color:#5a5aa7;color:#ffffff"
              class="button--blue"
            >Get Yearly Plan ($49.99)</Button>
          </template>
        </stripe-checkout>
        <br />
      </div>
      <div class="p-col-12 p-md-6 p-lg-6">
        <h2>CleanVid is a browser extension that will transform your chrome based browser into an automated video ads skipping machine.</h2>
        <br />
        <p
          class="paragraph"
        >$6.99 per month. Take advantage of our discount if you pay yearly. Yearly subscription starts at $49.99. A 40% saving!</p>
        <br />
        <br />
        <stripe-checkout
          ref="checkoutMonthlyRef"
          pk="pk_test_GOYwfBk7nZhol9yUB35Yr469"
          :items="itemsMonthly"
          :successUrl="successUrl"
          :cancelUrl="cancelUrl"
        >
          <template slot="checkout-button">
            <Button
              @click="checkoutMonthly"
              style="background-color:#5a5aa7;color:#ffffff"
              class="button--blue"
            >Get Monthly Plan ($6.99)</Button>
          </template>
        </stripe-checkout>
      </div>
    </div>
  </div>
</template>

<script>
import Button from "primevue/button";
import Logo from "~/components/Logo.vue";
import netlifyIdentity from "netlify-identity-widget";
import { mapActions } from "vuex";
import { StripeCheckout } from "vue-stripe-checkout";
netlifyIdentity.init();

export default {
  components: {
    Logo,
    StripeCheckout,
    Button,
  },
  data: () => ({
    loading: false,
    publishableKey: process.env.PUBLISHABLE_KEY,
    items: [
      {
        plan: "price_1HB6ykJZQIESMqe333HAeUY9",
        quantity: 1,
      },
    ],
    itemsMonthly: [
      {
        plan: "price_1HC1e6JZQIESMqe3CWJEbmff",
        quantity: 1,
      },
    ],
    successUrl: `${document.location.href}/success`,
    cancelUrl: `${document.location.href}`,
    home: location.href,
  }),
  methods: {
    ...mapActions({
      setUser: "user/setUser",
    }),
    checkoutYearly() {
      this.$refs.checkoutYearlyRef.redirectToCheckout();
    },
    checkoutMonthly() {
      this.$refs.checkoutMonthlyRef.redirectToCheckout();
    },
    triggerNetlifyIdentityAction(action) {
      if (action == "login" || action == "signup") {
        netlifyIdentity.open(action);
        netlifyIdentity.on(action, (user) => {
          this.setUser(user);
          netlifyIdentity.close();
        });
      } else if (action == "logout") {
        this.setUser(null);
        netlifyIdentity.logout();
        this.$router.push("/");
      }
    },
  },
};
</script>

<style>

.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
