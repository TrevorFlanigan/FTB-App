<template>
  <div class="sidebar">
    <!-- <logo width="80%" class="logo" draggable="false"/> -->
    <img src="../assets/logo_ftb.png" width="125px"/>
    <div class="nav-items flex-col">
      <nav-item :isActive="isActiveTab('news')" @click="goTo('news')"><font-awesome-icon icon="newspaper" size="lg" class="mr-3" />News</nav-item>
      <nav-item :isActive="isActiveTab('home')" @click="goTo('/')"><font-awesome-icon icon="home" size="lg" class="mr-3" />Home</nav-item>
      <nav-item :isActive="isActiveTab('modpacks') || isActiveTab('browseModpacks') || isActiveTab('thirdparty')" @click="goTo('modpacks')" :hasSub="true"><font-awesome-icon icon="box-open" size="lg" class="mr-3" />Modpacks</nav-item>
    </div>
    <div class="nav-items flex-col mt-auto mb-0">
      <nav-item :isActive="isActiveTab('settings')" @click="goTo('/settings')"><font-awesome-icon icon="cog" size="lg" class="mr-3" />Settings</nav-item>
      <!-- <nav-item :isActive="isActiveTab('modpacks')" @click="goTo('modpacks')"><font-awesome-icon icon="sign-out-alt" size="lg" class="mr-3" />Logout</nav-item> -->
    </div>
    <img src="../assets/ch-logo.svg" width="90%" class="mb-2 cursor-pointer" draggable="false" @click="openPromo()"/>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import NavItem from './nav/NavItem.vue';
import Logo from './Logo.vue';
import {shell} from 'electron';

@Component({components: {NavItem, Logo}})
export default class Sidebar extends Vue {

  public isActiveTab(tab: string): boolean {
    return tab === 'home' && this.$route.path === '/' ? true : this.$route.path.startsWith(`/${tab}`);
  }

  public goTo(page: string): void {
    // We don't care about this error!
    this.$router.push(page).catch((err) => { return; });
  }

  public openPromo(): void {
    shell.openExternal('https://creeperhost.net/applyPromo/FEEDME');
  }
}
</script>

<style scoped lang="scss">
    .sidebar {
        height: 100%;
        flex: 1;
        background-color: var(--color-navbar);
        display: flex;
        align-items: center;
        justify-content: flex-start;
        flex-direction: column;
    }
    .logo {
      margin-top: 10px;
      margin-bottom: 20px;
    }
    .nav-items {
      width: 100%;
      display: flex;
      cursor: pointer;
    }
</style>
