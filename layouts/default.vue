<template>
  <div>
    <Menubar :model="items">
      <template #start>
        <img
          alt="logo"
          src="https://cleanvid.org/wp-content/uploads/2020/06/cleanvid-logo.png"
          height="100"
          class="p-mr-2"
          style="padding-right:50%"
        />
      </template>
      <template #end>
        <div
          v-if="isLoggedIn"
          v-on:click="triggerNetlifyIdentityAction('logout')"
          class="button--blue-inverted"
        >Logout</div>
        <div
          v-else
          v-on:click="triggerNetlifyIdentityAction('login')"
          class="button--blue-inverted"
        >Login</div>
        <nuxt-link to="/protected" class="button--blue-inverted">Get Started</nuxt-link>
      </template>
    </Menubar>
    <nuxt />
    <div class="footer">
      <div class="p-grid">
        <div class="p-col" style="background-color:#261b48;">
          <div class="p-grid" style="padding-top:20px;">
            <div class="p-col" style="text-align: -webkit-center;">
              <Menu :model="itemsProducts" />
            </div>
            <div class="p-col" style="text-align: -webkit-center;">
              <Menu :model="itemsCompany" />
            </div>
            <div class="p-col" style="text-align: -webkit-center;">
              <Menu :model="itemsInvestors" />
            </div>
          </div>
        </div>
        <div class="p-col-5" style="background-color: #32245e;">
          <div class="contact-form">
            <contact-form></contact-form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapActions, mapState } from "vuex";
import ContactForm from "./../components/ContactForm";
import netlifyIdentity from "netlify-identity-widget";
netlifyIdentity.init();

export default {
  name: "Default",
  components: {
    ContactForm,
  },
  data() {
    return {
      itemsCompany: [
        {
          label: "Company",
          items: [
            {
              label: "About Us",
            },
            {
              label: "Blog",
            },
            {
              label: "News",
            },
            {
              label: "Careers",
            },
            {
              label: "Contact Us",
            },
          ],
        },
      ],
      itemsProducts: [
        {
          label: "Products",
          items: [
            {
              label: "Skip Ads Module",
            },
            {
              label: "Filtering Module",
            },
          ],
        },
      ],
      itemsInvestors: [
        {
          label: "Investor",
          items: [
            {
              label: "Invest",
            },
            {
              label: "Pitch Deck",
            },
          ],
        },
      ],
      items: [
        {
          label: "Home",
          items: [
            {
              label: "Support",
              to: "/support",
            },
          ],
        },
        {
          label: "Ad Skipping",
          items: [
            {
              label: "IMDB",
              url: "http://imdbtv.com",
            },
            {
              label: "Roku",
              url: "https://therokuchannel.roku.com",
            },
            {
              label: "YouTube",
              url: "https://youtube.com",
            },
            {
              label: "YouTube TV",
              url: "https://tv.youtube.com/",
            },
            {
              label: "Hulu",
              url: "https://hulu.com",
            },
            {
              label: "Sling",
              url: "https://www.sling.com/",
            },
            {
              label: "Peacock TV",
              url: "https://www.peacocktv.com/",
            },
            {
              label: "CBS",
              url: "https://www.cbs.com/",
            },
            {
              label: "ABC",
              url: "https://www.abc.com/",
            },
            {
              label: "STARZ",
              url: "https://www.starz.com/",
            },
            {
              label: "HBO Max",
              url: "https://www.hbomax.com/",
            },
            {
              label: "HBO Now",
              url: "https://www.hbonow.com/",
            },
            {
              label: "Crackle",
              url: "https://www.crackle.com/",
            },
            {
              label: "Tubi",
              url: "http://tubitv.com/",
            },
            {
              label: "Pluto TV",
              url: "http://pluto.tv/",
            },
            {
              label: "Popcorn Flix",
              url: "http://popcornflix.com/",
            },
            {
              label: "Espn",
              url: "https://espn.com/",
            },
          ],
        },
      ],
    };
  },
  computed: mapState({
    isLoggedIn: (state) => state.user.currentUser,
  }),
  methods: {
    ...mapActions({
      setUser: "user/setUser",
    }),
    triggerNetlifyIdentityAction(action) {
      if (action == "login" || action == "signup") {
        netlifyIdentity.open(action);
        netlifyIdentity.on(action, (user) => {
          this.setUser(user);
          netlifyIdentity.close();
          this.$router.push("/profile");
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
html {
  font-family: 'Source Sans Pro', -apple-system, BlinkMacSystemFont, 'Segoe UI',
    Roboto, 'Helvetica Neue', Arial, sans-serif;
  font-size: 16px;
  word-spacing: 1px;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  -moz-osx-font-smoothing: grayscale;
  -webkit-font-smoothing: antialiased;
  box-sizing: border-box;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}

.p-menubar {
    padding: 0.5rem;
    background: #e8eff5;
    color: #333333;
    border: 1px solid #c8c8c8;
    border-radius: 3px;
}

.p-menu {
    padding: 0;
    background:transparent;
    color: #ffffff;
    border: 1px solid transparent;
    border-radius: 3px;
    width: 12.5rem;
}



.p-menu .p-submenu-header {
    margin: 0;
    padding: 0.857rem;
    color: #ffffff;
    background: transparent;
    font-weight: 700;
    border-top-right-radius: 3px;
    border-top-left-radius: 3px;
    text-align: left;
}

.p-menu .p-menuitem-link .p-menuitem-text {
    color: #ffffff;
}

.contact-form {
  background-color: #32245e;
    height: 200px;
    width: 110%;
    position: relative;
    border-radius: 20px 0px 0px 0px;
    top: -40px;
    left: -10px;
}

.footer-h4 {
  color: #f0f0ff;
  font-size: 1rem;
  text-align: center;
}

.p-menubar-root-list {
  margin: auto;
}

.p-menubar-button {
  position: absolute;
  right: 50px;
}

.footer {
  padding-top:50px;
}

.button--green {
  background-color: #3b8070;
  cursor: pointer;
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #3b8070;
  color: #ffffff;
  text-decoration: none;
  padding: 10px 30px;
}

.button--green:hover {
  color: #ffffff;
  background-color:#000000;
  
}

.button--blue {
  cursor: pointer;
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #5a5aa7;
  color: #35495e;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
}

.button--blue:hover {
  color: #fff;
  background-color: #5a5aa7;
}

.button--blue-inverted {
  cursor: pointer;
  display: inline-block;
  border-radius: 4px;
  border: 1px solid #5a5aa7;
  color: #ffffff;
  text-decoration: none;
  padding: 10px 30px;
  margin-left: 15px;
  background-color: #5a5aa7;
}

.button--blue-inverted:hover {
  color: #000;
  background-color: transparent;
}
</style>
