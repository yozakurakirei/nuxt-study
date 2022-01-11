<template>
  <v-app>
    <v-navigation-drawer app v-model="drawer" clipped class="hamburger">
      <v-container>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="title grey--text text--darken-2">
               <h3><a href="/">Mana</a></h3>
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        
        <v-divider></v-divider>

        <v-list nav dense>
          <v-list-item v-for="nav_list in nav_lists" :key="nav_list.name" :to="nav_list.link">
            <template v-slot: activator>
              <v-list-item-content>
                <v-list-item-title>{{ nav_list.name }}</v-list-item-title>
              </v-list-item-content>
            </template>
          </v-list-item>
        </v-list>
      </v-container>
    </v-navigation-drawer>

    <v-app-bar color="#fff" app clipped-left>
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-toolbar-title ><a href="/">Mana</a></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn color="#00A85F" class="white--text contact-btn" to="/contact">お問い合わせ</v-btn>
        <v-menu offset-y>
          <template v-slot:activator="{on}">
          <v-btn v-on="on" text>運営者情報</v-btn>
          </template>
          <v-list>
            <v-list-item v-for="admin in admins" :key="admin" :to="admin.link">
              <v-list-item-content class="drop__list">
                <v-list-item-title class="drop__list__item">{{ admin.name }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </v-list>
        </v-menu>
    </v-app-bar>

    <!-- main -->
    <v-main>
      <router-view />
    </v-main>

    <v-footer color="#00A85F" class="fotter" app>
      開発環境
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      drawer: null,
      admins: [
        {name: "GitHub", soto: "https://github.com/yozakurakirei"},
        {name: "Qiita"},
        {name: "ポートフォリオ"},
        {name: "お問い合わせ", link: "/contact"}
      ],
      nav_lists: [
        {name: "自社サービス", lists: ["フロントエンド", "バックエンド", "インフラ", "その他"]},
        {name: "Sler"},
        {name: "SES"},
        {name: "その他企業"},
        {name: "グラフで見てみる", link: "/graph"}
      ]
    }
  }
}
</script>

<style lang="scss">
.contact-btn {
  font-weight: 700 !important;
  margin-right: 1rem;
}

.drop__list {
  border-bottom: 2px solid #ccc;
  :hover {
    opacity: .7;
    cursor: pointer;
  }
  .drop__list__item {
    font-size: .8rem !important;
  }
}

.fotter {
  color: #fff !important;
}
</style>