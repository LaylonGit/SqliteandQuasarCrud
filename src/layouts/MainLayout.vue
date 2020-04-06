<template>
  <q-layout view="lHh Lpr lFf">
    <q-header>
      <q-toolbar class="row justify-between">
        <q-btn
          flat
          dense
          round
          icon="fas fa-arrow-left"
          aria-label="Menu"
        />
        <q-btn
          flat
          dense
          round
          icon="far fa-building"
          aria-label="Menu"
        />

      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>

export default {

  data () {
    return {
    }
  }
}
</script>
