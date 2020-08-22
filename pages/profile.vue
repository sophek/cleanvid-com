<template>
  <div style="padding:5%">
    <div class="p-grid">
      <div class="p-col">
        <div class="p-grid">
          <div class="p-col">
            <h3>Ad Tracker</h3>
          </div>
        </div>
        <div class="p-grid">
          <div class="p-col">
            <DataTable :value="adsSKipped">
              <Column field="service" header="Service"></Column>
              <Column field="count" header="# of Ads Skipped"></Column>
              <Column field="duration" header="Time Saved"></Column>
            </DataTable>
          </div>
        </div>
      </div>
    </div>
    <div class="p-grid">
      <div class="p-col">
        <div class="p-grid">
          <div class="p-col">
            <h3>Invoices</h3>
          </div>
        </div>
        <div class="p-grid">
          <div class="p-col">
            <DataTable :value="invoices">
              <Column field="dateOfInvoice" header="Subscription Date"></Column>
              <Column field="amount" header="Amount"></Column>
              <Column field="recieptId" header="Reciept"></Column>
            </DataTable>
          </div>
        </div>
      </div>
    </div>

    <stripe-checkout
      ref="checkoutRef"
      pk="pk_test_GOYwfBk7nZhol9yUB35Yr469"
      :items="items"
      :successUrl="successUrl"
      :cancelUrl="cancelUrl"
    >
      <template slot="checkout-button">
        <Button @click="checkout" class="button--blue">Check Out</Button>
      </template>
    </stripe-checkout>
    <div class="links">
      <nuxt-link to="/" class="button--green">Home</nuxt-link>
      <div v-on:click="triggerNetlifyIdentityAction('logout')" class="button--blue">Logout</div>
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
    adsSKipped: [{ service: "youtube", count: 10, duration: 12.56 }],
    invoices: [
      { dateOfInvoice: "09-14-2020", amount: 39.0, recieptId: "2ZSISDH" },
    ],
    loading: false,
    publishableKey: process.env.PUBLISHABLE_KEY,
    items: [
      {
        plan: "price_1HB6ykJZQIESMqe333HAeUY9",
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
    checkout() {
      this.$refs.checkoutRef.redirectToCheckout();
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
  middleware({ store, redirect }) {
    if (!store.state.user.currentUser) {
      return redirect("/");
    }
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
