<template>
  <nav v-show="isNavBarVisible" id="navbar-main" class="navbar is-fixed-top">
    <div class="navbar-brand">
      <a :title="toggleTooltip" class="navbar-item is-desktop-icon-only is-hidden-touch" @click.prevent="menuToggle">
        <b-icon :icon="menuToggleIcon" />
      </a>
      <a class="navbar-item is-hidden-desktop" @click.prevent="menuToggleMobile">
        <b-icon :icon="menuToggleMobileIcon" />
      </a>
      <div class="navbar-item no-left-space">
        <div class="control">
          <input class="input" placeholder="Search everywhere...">
        </div>
      </div>
    </div>
    <div class="navbar-brand is-right">
      <a class="navbar-item navbar-item-menu-toggle is-hidden-desktop" @click.prevent="updatesToggle">
        <b-icon icon="bell" custom-size="default" />
      </a>
      <a class="navbar-item navbar-item-menu-toggle is-hidden-desktop" @click.prevent="menuNavBarToggle">
        <b-icon :icon="menuNavBarToggleIcon" custom-size="default" />
      </a>
    </div>
    <div class="navbar-menu fadeIn animated faster" :class="{'is-active':isMenuNavBarActive}">
      <div class="navbar-end">
        <nav-bar-menu class="has-divider has-user-avatar">
          <user-avatar />
          <div class="is-user-name">
            <span>{{ userName }}</span>
          </div>

          <div slot="dropdown" class="navbar-dropdown">
            <nuxt-link to="/profile" class="navbar-item" exact-active-class="is-active">
              <b-icon icon="account" custom-size="default" />
              <span>My Profile</span>
            </nuxt-link>
            <a class="navbar-item">
              <b-icon icon="settings" custom-size="default" />
              <span>Settings</span>
            </a>
            <a class="navbar-item">
              <b-icon icon="email" custom-size="default" />
              <span>Messages</span>
            </a>
            <hr class="navbar-divider">
            <a class="navbar-item">
              <b-icon icon="logout" custom-size="default" />
              <span>Log Out</span>
            </a>
          </div>
        </nav-bar-menu>
        <nav-bar-menu class="has-divider">
          <b-icon icon="menu" custom-size="default" />
          <span>Sample Menu</span>
          <div slot="dropdown" class="navbar-dropdown">
            <nuxt-link to="/profile" class="navbar-item" exact-active-class="is-active">
              <b-icon icon="account" custom-size="default" />
              <span>My Profile</span>
            </nuxt-link>
            <a class="navbar-item">
              <b-icon icon="settings" custom-size="default" />
              <span>Settings</span>
            </a>
            <a class="navbar-item">
              <b-icon icon="email" custom-size="default" />
              <span>Messages</span>
            </a>
            <hr class="navbar-divider">
            <a class="navbar-item">
              <b-icon icon="logout" custom-size="default" />
              <span>Log Out</span>
            </a>
          </div>
        </nav-bar-menu>
        <a class="navbar-item has-divider is-desktop-icon-only" title="Dark mode" @click="darkModeToggle">
          <b-icon :icon="darkModeToggleIcon" custom-size="default" />
          <span>Dark mode</span>
        </a>
        <a href="https://justboil.me/bulma-admin-template/null-nuxt" class="navbar-item has-divider is-desktop-icon-only" title="About">
          <b-icon icon="help-circle-outline" custom-size="default" />
          <span>About</span>
        </a>
        <a class="navbar-item has-divider is-desktop-icon-only" :class="{'is-active':isAsideRightVisible}" title="Updates" @click.prevent="updatesToggle">
          <b-icon icon="bell" custom-size="default" :class="{'has-update-mark':hasUpdates}" />
          <span>Updates</span>
        </a>
        <a class="navbar-item is-desktop-icon-only" title="Log out" @click="logout">
          <b-icon icon="logout" custom-size="default" />
          <span>Log out</span>
        </a>
      </div>
    </div>
  </nav>
</template>

<script>
import { mapState } from 'vuex'
import NavBarMenu from '@/components/NavBarMenu'
import UserAvatar from '@/components/UserAvatar'

export default {
  name: 'NavBar',
  components: {
    UserAvatar,
    NavBarMenu
  },
  data () {
    return {
      isMenuNavBarActive: false
    }
  },
  computed: {
    menuNavBarToggleIcon () {
      return (this.isMenuNavBarActive) ? 'close' : 'dots-vertical'
    },
    menuToggleMobileIcon () {
      return this.isAsideMobileExpanded ? 'backburger' : 'forwardburger'
    },
    menuToggleIcon () {
      return this.isAsideExpanded ? 'backburger' : 'forwardburger'
    },
    toggleTooltip () {
      return this.isAsideExpanded ? 'Collapse' : 'Expand'
    },
    darkModeToggleIcon () {
      return this.isDarkModeActive ? 'white-balance-sunny' : 'weather-night'
    },
    ...mapState([
      'isNavBarVisible',
      'isAsideExpanded',
      'isAsideMobileExpanded',
      'isAsideRightVisible',
      'isDarkModeActive',
      'userName',
      'hasUpdates'
    ])
  },
  methods: {
    menuToggle () {
      this.$store.commit('asideStateToggle')
    },
    menuToggleMobile () {
      this.$store.commit('asideMobileStateToggle')
    },
    menuNavBarToggle () {
      this.isMenuNavBarActive = (!this.isMenuNavBarActive)
    },
    updatesToggle () {
      this.$store.commit('asideRightToggle')
    },
    darkModeToggle () {
      this.$store.commit('darkModeToggle')
    },
    logout () {
      this.$buefy.snackbar.open({
        message: 'Log out clicked',
        queue: false
      })
    }
  }
}
</script>
