<template>
  <main>
    <!-- App Header -->
    <AppHeader title="Home"></AppHeader>

    <div class="container is-fluid">
      <!-- Search -->
      <div class="field">
        <p class="control has-icons-left">
          <label>
            <input class="input is-rounded" type="text" placeholder="Search">
            <span class="icon is-left">
              <ion-icon name="search-circle-outline" size="large"></ion-icon>
            </span>
          </label>
        </p>
      </div>

      <!-- Home Navigation -->
      <nav class="level is-mobile is-marginless">
        <div class="level-left">
          <div class="level-item has-text-centered">
            <router-link to="/home">
              <div class="title">
                <div class="icon is-large">
                  <ion-icon name="people-outline" size="large"></ion-icon>
                </div>
              </div>
            </router-link>
          </div>
          <div class="level-item has-text-centered">
            <router-link to="/home">
              <div class="title">
                <div class="icon is-large">
                  <ion-icon name="person-add-outline" size="large"></ion-icon>
                </div>
              </div>
            </router-link>
          </div>
        </div>
        <div class="level-right">
          <div class="level-item has-text-centered">
            <div v-on:click="changeTab(1)">
              <div class="title">
                <div class="icon is-large">
                  <ion-icon name="settings-outline" size="large"
                            v-bind:color="tab === 1 ? 'primary' : 'dark'"></ion-icon>
                </div>
              </div>
            </div>
          </div>
        </div>
      </nav>

      <!-- Feed -->
      <section class="section" v-if="tab === 0">
        <h3 class="title is-size-5">Feed</h3>
        <p class="is-size-7" v-if="activities.length <= 0">Your activity will be displayed here.</p>
        <div v-else>
          <FeedItem v-for="activity in activities" v-bind:key="activity._id" v-bind:activity="activity"></FeedItem>
        </div>
      </section>

      <!-- Settings -->
      <section class="section" v-if="tab === 1">
        <nav class="level is-mobile is-marginless">
          <div class="level-left">
            <div class="level-item has-text-centered">
              <h3 class="title is-size-5">Settings</h3>
            </div>
          </div>
          <div class="level-right">
            <div class="level-item has-text-centered">
              <div v-on:click="changeTab(0)">
                <div class="title">
                  <div class="icon is-large">
                    <ion-icon name="close-circle-outline" size="large"></ion-icon>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </nav>
      </section>
    </div>

    <!-- App Navbar -->
    <AppNavbar></AppNavbar>
  </main>
</template>

<script>
import AppHeader from '../components/AppHeader'
import AppNavbar from '../components/AppNavbar'
import FeedItem from '../components/FeedItem'

export default {
  name: 'Home',
  components: {
    FeedItem,
    AppHeader,
    AppNavbar
  },
  computed: {
    activities () {
      return this.$store.getters['auth/tokenData'].activities
    }
  },
  data: function () {
    return {
      tab: 0
    }
  },
  methods: {
    changeTab: function (tab) {
      this.tab = tab
    }
  }
}
</script>
