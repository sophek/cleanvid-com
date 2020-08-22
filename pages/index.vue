<template>
  <div style="padding:0">
    <div class="p-grid" style="background-color:#ffffff;padding:5%">
      <div class="p-col-12 p-md-6 p-lg-6">
        <h2>Introducing CleanVid, the world’s first fully automated multiple platform video ad-skipping service.</h2>
        <p
          class="paragraph"
        >For $49.99 per year, you have the abliity to skips all the ads you want on over 15 ad supported streaming services.</p>
        <nuxt-link to="/protected" class="button--blue-inverted">Get Started</nuxt-link>
        <br />

        <img src="./../assets/undraw_things_to_say_ewwb-300x241.png" />
      </div>
      <div class="p-col-12 p-md-6 p-lg-6">
        <img src="./../assets/undraw_media_player.png" style="width:75%" />
        <h2>CleanVid is a browser extension that will transform your chrome based browser into an automated video ads skipping machine.</h2>
        <br />
      </div>
    </div>
    <div class="p-grid" style="background-color:#e8eff5;padding:5%">
      <div class="p-col">
        <h2>Automatically Skip Video Ads</h2>
        <br />
        <p
          class="paragraph"
        >Skip video ads automatically on Youtube, Youtube TV, Hulu, Peacock TV, ABC, CBS, Starz, HBO Max, HBO Now, IMDB TV, Tubi, Pluto TV, Sony Crackle, Roku, Popcorn Flix and SlingTV. By installing the browser extension, you unlock the power to elimante ads automatically. Some of theses services charge a premium to remove ads. Our extension removes all of them. We are constantly adding new ones, please check often.</p>
        <br />

        <div class="p-grid">
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/abc-logo.png" class="logo-width" style="width:75px" />
          </div>

          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/cbs-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/youtube-logo.svg" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/youtube-tv-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/hulu-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/peacocktv-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/hbomax-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/hbonow-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/sling-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/starz-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/tubi-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/pluto-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/crackle-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/imdb-logo.png" class="logo-width" />
          </div>
          <div class="p-col-12 p-md-6 p-lg-3">
            <img src="./../assets/logos/popcornflix-logo.png" class="logo-width" />
          </div>
        </div>
      </div>
    </div>
    <div class="p-grid" style="background-color:#ffffff;padding:5%">
      <div class="p-col">
        <img src="./../assets/undraw_youtube_tutorial_2gn3-150x150.png" />
        <h3>Automatically Skip Video Ads</h3>
        <br />
        <p>Automatically skip video ads! Sit back enjoy your videos without interruption, even fast forward live TV.</p>
        <br />
        <nuxt-link to="/protected" class="button--blue-inverted">Get Started</nuxt-link>
        <br />
      </div>
      <div class="p-col">
        <img src="./../assets/undraw_placeholders_rklh-150x150.png" />
        <h3>Fast Forward Live TV</h3>
        <br />
        <p>
          Press the
          <kbd>/</kbd> key to fast forward and cycle to 4x speed. Press the
          <kbd>s</kbd> key to skip ahead 30 seconds. Press the
          <kbd>z</kbd> key to skip to the end.
        </p>
      </div>
      <div class="p-col">
        <img src="./../assets/undraw_time_management_30iu.png" style="width:200px" />
        <h3>Keep Track of the time you saved using CleanVid</h3>
        <br />
        <p>More of what you want. Less of what you don't. Take back the minutes of your life... with Cleanvid.</p>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from "~/components/Logo.vue";
import netlifyIdentity from "netlify-identity-widget";
import { mapActions, mapState } from "vuex";
import { StripeCheckout } from "vue-stripe-checkout";
netlifyIdentity.init();

export default {
  components: {
    Logo,
    StripeCheckout,
  },
  computed: mapState({
    isLoggedIn: (state) => state.user.currentUser,
  }),
  data: () => ({
    services: [
      {
        label: "IMDB",
        url: "http://imdbtv.com",
        logo: "~/assets/logos/abc-logo.png",
      },
      {
        label: "Roku",
        url: "https://therokuchannel.roku.com",
        logo: "/assets/logos/roku-logo.png",
      },
      {
        label: "YouTube",
        url: "https://youtube.com",
        logo: "./../assets/logos/youtube-logo.svg",
      },
      {
        label: "YouTube TV",
        url: "https://tv.youtube.com/",
        logo: "./../assets/logos/youtube-tv-logo.png",
      },
      {
        label: "Hulu",
        url: "https://hulu.com",
        logo: "./../assets/logos/hulu-logo.png",
      },
      {
        label: "Sling",
        url: "https://www.sling.com/",
        logo: "./../assets/logos/sling-logo.png",
      },
      {
        label: "Peacock TV",
        url: "https://www.peacocktv.com/",
        logo: "./../assets/logos/peacocktv-logo.png",
      },
      {
        label: "CBS",
        url: "https://www.cbs.com/",
        logo: "./../assets/logos/cbs-logo.png",
      },
      {
        label: "ABC",
        url: "https://www.abc.com/",
        logo: "./../assets/logos/abc-logo.png",
      },
      {
        label: "Starz",
        url: "https://www.starz.com/",
        logo: "./../assets/logos/starz-logo.png",
      },
      {
        label: "HBO Max",
        url: "https://www.hbomax.com/",
        logo: "./../assets/logos/hbomax-logo.png",
      },
      {
        label: "HBO Now",
        url: "https://www.hbonow.com/",
        logo: "./../assets/logos/hbonow-logo.png",
      },
      {
        label: "Crackle",
        url: "https://www.crackle.com/",
        logo: "./../assets/logos/crackle-logo.png",
      },
      {
        label: "Tubi",
        url: "http://tubitv.com/",
        logo: "./../assets/logos/tubi-logo.png",
      },
      {
        label: "Pluto TV",
        url: "http://pluto.tv/",
        logo: "./../assets/logos/pluto-logo.png",
      },
      {
        label: "Popcorn Flix",
        url: "http://popcornflix.com/",
        logo: "./../assets/logos/popcornflix-logo.png",
      },
      {
        label: "Espn",
        url: "https://espn.com/",
        logo: "./../assets/logos/espn-logo.png",
      },
    ],
    loading: false,
    publishableKey: process.env.PUBLISHABLE_KEY,
    items: [
      {
        plan: "price_1HB6ykJZQIESMqe333HAeUY9",
        quantity: 1,
      },
    ],
    successUrl: `${document.location.href}success.html`,
    cancelUrl: `${document.location.href}`,
    home: location.href,
  }),
  methods: {
    checkout() {
      this.$refs.checkoutRef.redirectToCheckout();
    },
    ...mapActions({
      setUser: "user/setUser",
    }),
    circumvent() {
      window.localStorage.setItem("user", true);
      location.reload(true);
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

.logo-width {
  width: 150px;
}

.paragraph {
  padding: 10px 0px 20px 0px;
  font-size: 1.25rem;
}

kbd {
    margin: 0px 0.1em;
    padding: 0.1em 0.6em;
    border-radius: 3px;
    border: 1px solid rgb(204,204,204);
    color: rgb(51,51,51);
    line-height: 1.4;
    font-family: Arial,Helvetica,sans-serif;
    font-size: 10px;
    display: inline-block;
    box-shadow: 0px 1px 0px rgba(0,0,0,0.2), inset 0px 0px 0px 2px #ffffff;
    background-color: rgb(247,247,247);
    -moz-box-shadow: 0 1px 0px rgba(0,0,0,0.2),0 0 0 2px #ffffff inset;
    -webkit-box-shadow: 0 1px 0px rgba(0,0,0,0.2), 0 0 0 2px #ffffff inset;
    -moz-border-radius: 3px;
    -webkit-border-radius: 3px;
    text-shadow: 0 1px 0 #fff;
}

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
  line-height: 1;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.greetings {
  font-family: 'Quicksand', 'Source Sans Pro', -apple-system, BlinkMacSystemFont,
    'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-weight: 400;
}

.links {
  padding-top: 15px;
}
</style>
