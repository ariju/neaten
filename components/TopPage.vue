<template>
  <v-app>
    <v-navigation-drawer app v-model="drawer" clipped>
      <v-container>
        <v-list-item>
          <v-btn text nuxt-link to="/" class="m-5"
            ><v-icon>mdi-home</v-icon>HOME トップページ</v-btn
          >
        </v-list-item>
        <v-divider></v-divider>
        <v-list-item>
          <v-btn text nuxt-link to="/desk" class="m-5"
            ><v-icon>mdi-desk</v-icon>desk 机</v-btn
          >
        </v-list-item>
        <v-divider></v-divider>
        <v-list-item>
          <v-btn text nuxt-link to="/wardrobe" class="m-5"
            ><v-icon>mdi-wardrobe</v-icon>wardrobe タンス</v-btn
          >
        </v-list-item>
      </v-container>
    </v-navigation-drawer>
    <v-app-bar color="#C0C0C0" dark app clipped-left>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
      <v-toolbar-title>Neaten</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-toolbar-items>
        <v-menu offset-y>
          <template v-slot:activator="{ on }">
            <v-btn v-on="on" text>Support<v-icon>mdi-menu-down</v-icon></v-btn>
          </template>
          <v-list dense nav>
            <v-subheader>Get help</v-subheader>
            <v-list-item>
              <v-list-item-content>
                <v-list-item>
                  <v-btn text @click="login"
                    ><v-icon>mdi-login</v-icon>ログイン</v-btn
                  >
                </v-list-item>
                <v-list-item>
                  <v-btn text @click="logout"
                    ><v-icon>mdi-logout</v-icon>ログアウト</v-btn
                  >
                </v-list-item>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-menu>
      </v-toolbar-items>
    </v-app-bar>
    <div class="content">
      <div class="content_title">
        <div class="TextAnime1">
          <span
            v-for="(t, index) in text"
            :key="index"
            class="item"
            :style="{ animationDelay: index * 100 + 'ms' }"
            v-text="t"
          />
        </div>

        <nuxt />
      </div>
    </div>
    <v-card>
      <h2></h2>
    </v-card>
    <v-footer color="#C0C0C0" dark app>
      Neaten
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      text: "収納を管理しよう"
    };
  },
  methods: {
    login() {
      const provider = new this.$firebase.auth.GoogleAuthProvider();
      this.$fireAuth
        .signInWithRedirect(provider)
        .then(() => {
          console.log("ログイン");
        })
        .catch(error => {
          console.log(error);
        });
    },
    logout() {
      this.$fireAuth
        .signOut()
        .then(() => {
          console.log("ログアウト");
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
.content {
  height: 664px;
  display: flex;
  width: 100%;
  background-size: cover;
  background-image: url("~@/assets/images/hiki.jpg");
  position: relative;
}
.content_title {
  color: black;
  margin: auto;
  height: 177px;
  width: 643px;
  padding-left: 48px;
  font-weight: bold;
  font-family: serif;
  letter-spacing: 2px;
}
@keyframes text-in {
  0% {
    transform: translate(0, -20px);
    opacity: 0;
  }
}
.item {
  display: inline-block;
  min-width: 0.3em;
  font-size: 3rem;
  animation: text-in 0.8s cubic-bezier(0.22, 0.15, 0.25, 1.43) 0s backwards;
}
</style>
