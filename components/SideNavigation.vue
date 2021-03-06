<template>
  <div class="SideNavigation">
    <div class="SideNavigation-HeadingContainer sp-flex">
      <v-icon
        class="SideNavigation-HeadingIcon pc-none"
        :aria-label="$t('Navi Open')"
        @click="openNavi"
      >
        mdi-menu
      </v-icon>
      <nuxt-link to="/" class="SideNavigation-HeadingLink">
        <div class="SideNavigation-Logo">
          <img src="/logo.png" :alt="$t('MiePrefecture')" />
        </div>
        <h1 class="SideNavigation-Heading">
          {{ $t('COVID-19') }}<br />{{ $t('Measures site') }}
        </h1>
      </nuxt-link>
    </div>
    <v-divider class="SideNavigation-HeadingDivider" />
    <div class="sp-none" :class="{ open: isNaviOpen }">
      <v-icon
        class="SideNavigation-ListContainerIcon pc-none"
        :aria-label="$t('Navi Close')"
        @click="closeNavi"
      >
        mdi-close
      </v-icon>
      <v-list :flat="true">
        <v-container
          v-for="(item, i) in items"
          :key="i"
          class="SideNavigation-ListItemContainer"
          @click="closeNavi"
        >
          <ListItem :link="item.link" :icon="item.icon" :title="item.title" />
          <v-divider v-show="item.divider" class="SideNavigation-Divider" />
        </v-container>
      </v-list>
      <div class="SideNavigation-HeadingDivider-Footer">
        <a href="https://www.sakura.ad.jp/">
          <img src="../static/sakura-image.png" alt="さくらインターネット" />
        </a>
      </div>
    </div>
  </div>
</template>

<i18n>
{
  "ja": {
    "Navi Open": "サイドメニュー項目を開く",
    "Navi Close": "サイドメニュー項目を閉じる",
    "COVID-19": "新型コロナウイルス感染症",
    "Measures site": "対策サイト（非公式）",
    "MiePrefecture": "三重県",
    "Tokyo COVID-19 Task Force": "新型コロナウイルス感染症対策本部",
    "The latest updates": "県内の最新感染動向",
    "for Families with children": "お子様をお持ちの皆様へ",
    "for Citizens": "県民の皆様へ",
    "for Enterprises and Employees": "企業の皆様・はたらく皆様へ",
    "Government official website": "三重県公式ホームページ",
    "Message from Governor Suzuki": "知事からのメッセージ",
    "About us": "当サイトについて",
    "Ivents Info": "新型コロナウイルス感染症に係る県主催イベントの中止・延期情報",
    "Facility Info": "新型コロナウイルス感染症に係る県有施設の休館情報",
    "Other local government sites":"他自治体の対策サイト",
    "Mie Coronavirus Countermeasures Official LINE":"三重県コロナウイルス対策公式LINE"
  }
}
</i18n>

<script>
import ListItem from '@/components/ListItem'

export default {
  components: {
    ListItem
  },
  props: {
    isNaviOpen: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    items() {
      return [
        {
          icon: 'mdi-chart-timeline-variant',
          title: this.$t('The latest updates'),
          link: '/'
        },
        {
          icon: 'parent',
          title: this.$t('for Families with children'),
          link: '/parent'
        },
        {
          icon: 'mdi-account-multiple',
          title: this.$t('for Citizens'),
          link: 'https://www.pref.mie.lg.jp/YAKUMUS/HP/m0068000066.htm#006'
        },
        {
          icon: 'mdi-domain',
          title: this.$t('for Enterprises and Employees'),
          link: '/worker',
          divider: true
        },
        {
          title: this.$t('Ivents Info'),
          link: 'https://www.pref.mie.lg.jp/KI2KANRI/HP/m0101300022.htm'
        },
        {
          title: this.$t('Facility Info'),
          link: 'https://www.pref.mie.lg.jp/YAKUMUS/HP/m0068000067_00004.htm'
        },
        {
          title: this.$t('Message from Governor Suzuki'),
          link: 'https://www.pref.mie.lg.jp/YAKUMUS/HP/m0068000067_00006.htm'
        },
        {
          title: this.$t('About us'),
          link: '/about'
        },
        {
          title: this.$t('Government official website'),
          link: 'https://www.pref.mie.lg.jp/'
        },
        {
          title: this.$t('Mie Coronavirus Countermeasures Official LINE'),
          link: 'https://www.pref.mie.lg.jp/YAKUMUS/HP/m0068000078.htm',
          divider: true
        },
        {
          title: this.$t('Other local government sites'),
          link:
            'https://github.com/tokyo-metropolitan-gov/covid19/blob/development/FORKED_SITES.md#readme'
        }
      ]
    },
    isClass() {
      return item => (item.title.charAt(0) === '【' ? 'kerningLeft' : '')
    }
  },
  methods: {
    openNavi() {
      this.$emit('openNavi')
    },
    closeNavi() {
      this.$emit('closeNavi')
    }
  }
}
</script>

<style lang="scss" scoped>
.SideNavigation {
  position: relative;
  height: 100%;
  background: $white;
  box-shadow: 0px 0px 2px rgba(0, 0, 0, 0.15);
  &-HeadingContainer {
    padding: 1.25em 0 1.25em 1.25em;
    align-items: center;
    @include lessThan($small) {
      padding: 7px 0 7px 20px;
    }
  }
  &-HeadingIcon {
    margin-right: 16px;
  }
  &-HeadingLink {
    @include lessThan($small) {
      display: flex;
      align-items: center;
    }
    text-decoration: none;
  }
  &-ListContainerIcon {
    margin: 24px 16px 0;
  }
  &-ListItemContainer {
    padding: 2px 20px;
  }
  &-Logo {
    margin: 20px 16px 0 0;
    width: 110px;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-Heading {
    margin-top: 8px;
    font-size: 13px;
    color: #898989;
    padding: 0.5em 0;
    text-decoration: none;
    @include lessThan($small) {
      margin-top: 0;
    }
  }
  &-HeadingDivider {
    margin: 0px 20px 4px;
    @include lessThan($small) {
      display: none;
    }
    &-Footer {
      width: 100%;
      background-color: white;
      margin-bottom: 10px;
    }
  }
  &-Divider {
    margin: 12px 0;
  }
  &-Footer {
    padding: 20px;
    background-color: $white;
  }
  &-SocialLinkContainer {
    display: flex;
    & img {
      width: 30px;
      &:first-of-type {
        margin-right: 10px;
      }
    }
  }
  &-Copyright {
    display: block;
    margin-top: 10px;
    font-size: 8px;
    line-height: 1.2;
    color: $gray-1;
    font-weight: bold;
  }
}

.open {
  @include lessThan($small) {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    display: block !important;
    width: 100%;
    z-index: z-index-of(opened-side-navigation);
    background-color: $white;
    overflow: auto;
  }
}
@include largerThan($small) {
  .pc-none {
    display: none;
  }
}
@include lessThan($small) {
  .sp-flex {
    display: flex;
  }
  .sp-none {
    display: none;
  }
}
</style>
