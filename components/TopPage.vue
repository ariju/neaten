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
    <div class="head">
      <p>
        locate
      </p>
    </div>
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
    <!-- メイン２ -->
    <v-card height="680" class="main">
        <div class="row">
          <div class="col-lg-8 col-md-10 mx-auto">
            <div class="post-preview">
              <h1 class="post-title text-center ma-8 display-1 font-weight-bold">
                アプリ紹介
              </h1>
              <hr />
              <h2 class="post-subtitle ma-5 headline font-weight-bold">
                Neaten収納管理アプリ
              </h2>
              <p class="post-meta font-weight-bold mx-6 title">
                このアプリは私自信が机の中の物や
                タンスの中に何を入れたか管理したかった為製作した物です。
                例えば机の中にたまにしか使用しない書類等を収納して、
                何処に何を入れたか直ぐに見つけられるようにしたかった為です。
                タンスの中であれば着たい服が何処にあるかが分かれば便利だと思います。
              </p>
              <h2 class="text-center ma-6">アプリで出来ること</h2>
              <v-img
              src="https://picsum.photos/350/165?random"
              max-height="125"
              contain
              class="grey darken-4"
            ></v-img>
            </div>
          </div>
      </div>
    </v-card>
    <!-- フッター -->
    <v-footer flat tile color="#C0C0C0" class="white--text text-center">
      <v-card-text mr-5>
        <img 
        height="30"
        :src="require('@/assets/images/vuetify.svg')"
        class="mr-3"
        >
        <img 
        height="30"
        :src="require('@/assets/images/nuxt.png')"
        class="mr-3"
        >
        <img 
        height="30"
        :src="require('@/assets/images/firebase.png')"
        class="mr-3"
        >
        <img 
        height="30"
        :src="require('@/assets/images/github.png')"
        class="mr-3"
        >
        <v-divider class="mt-3"></v-divider>
        <v-card-text class="fot white--text mt-2">
          {{ new Date().getFullYear() }} — <strong>Neaten</strong>
        </v-card-text>
      </v-card-text>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      text: "Naetenは収納を管理するアプリです。"
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
.head {
  height: 120px;
  font-size: 50px;
  padding-top: 55px;
  font-weight: bold;
}
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
.fot {
  font-size: 30px;
}
.main {
  width: 100%;
  background-size: cover;
  background-color: #dddddd;
}
</style>
