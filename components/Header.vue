<template>
  <header>
  <v-app-bar color="white" app>
    <v-toolbar-title ><a href="/">Mana</a></v-toolbar-title>
    <v-tabs>
      <v-tab class="nav-links" v-for="nav_list in nav_lists" :key="nav_list.name" :to="nav_list.link" text>
        {{ nav_list.name }}
      </v-tab>
    </v-tabs>
    <v-spacer></v-spacer>
    <v-btn color="#00A85F" class="white--text contact-btn" to="/contact">お問い合わせ</v-btn>
    <v-app-bar-nav-icon @click="drawer=true"></v-app-bar-nav-icon>
  </v-app-bar>
  <v-navigation-drawer v-model="drawer" right fixed temporary>
    <v-container>
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="title grey--text text--darken-2">
            <h3><a href="/">Mana</a></h3>
          </v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-divider></v-divider>
      <v-list nav>
        <v-list-item v-for="nav_list in nav_lists" :key="nav_list.name" :to="nav_list.link">
          <template v-slot: activator text>
            <v-list-item-content>{{ nav_list.name }}</v-list-item-content>
          </template>
        </v-list-item>
      </v-list>
    </v-container>
  </v-navigation-drawer>
</header>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
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
      ],
    }
  }
}
</script>

<style lang="scss" scoped>
.v-toolbar__title {
  overflow: visible !important;
  margin-right: 1rem !important;
}

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

// responsive
.v-app-bar__nav-icon {
  @include display_pc {
    display: none !important;
  }
}

.v-tabs {
  display: none;

  @include display_pc {
    display: block !important;
  }

  :hover {
    background: none;
  }
}

</style>