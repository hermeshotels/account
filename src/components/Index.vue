<template>
  <q-layout>

    <div slot="header" class="toolbar">
      <button class="hide-on-drawer-visible" @click="$refs.leftDrawer.open()">
        <i>menu</i>
      </button>
      <q-toolbar-title :padding="1">
        ErmesScout
      </q-toolbar-title>
    </div>

    <q-tabs slot="navigation">
      <q-tab icon="domain" route="/hotel/list" exact replace>Hotels</q-tab>
      <q-tab icon="compare_arrows" route="/channel/list" exact replace>Channel</q-tab>
    </q-tabs>

    <q-drawer left-side swipe-only ref="leftDrawer">
      <div class="toolbar light">
        <q-toolbar-title :padding="1">
            Right-side Drawer
        </q-toolbar-title>
      </div>

      <p style="padding: 25px;" class="text-grey-7">
        This is yet another Drawer that does not gets displayed alongside content on
        bigger screens.
      </p>
    </q-drawer>

    <router-view class="layout-view"></router-view>

  </q-layout>
</template>

<script>
</script>

<style lang="styl">
.logo-container
  width 192px
  height 268px
  perspective 800px
  position absolute
  top 50%
  left 50%
  transform translateX(-50%) translateY(-50%)
.logo
  position absolute
  transform-style preserve-3d
</style>
