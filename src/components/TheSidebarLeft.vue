<template>
  <v-navigation-drawer
    app
    temporary
    :value="isLeftSidebarOpen"
    disable-route-watcher
    @input="SET_LEFT_SIDEBAR_OPEN"
  >
    <v-list-item v-if="GET_PLEX_USER">
      <v-list-item-avatar>
        <v-img
          :src="GET_PLEX_USER.thumb"
        />
      </v-list-item-avatar>

      <v-list-item-content>
        <v-list-item-title style="font-weight: bold;">
          {{ GET_PLEX_USER.username }}
        </v-list-item-title>
      </v-list-item-content>
    </v-list-item>
    <v-divider />

    <v-list
      dense
      nav
    >
      <TheSettingsDialog v-slot="{ on, attrs }">
        <v-list-item
          v-bind="attrs"
          v-on="on"
        >
          <v-list-item-icon>
            <v-icon>settings</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Settings</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </TheSettingsDialog>

      <v-list-item
        :router="true"
        :to="{ name: 'SignOut' }"
      >
        <v-list-item-icon>
          <v-icon>cancel</v-icon>
        </v-list-item-icon>

        <v-list-item-content>
          <v-list-item-title>Sign out</v-list-item-title>
        </v-list-item-content>
      </v-list-item>

    </v-list>
  </v-navigation-drawer>
</template>

<script>
import { mapGetters, mapMutations, mapState } from 'vuex';

export default {
  name: 'TheSidebarLeft',

  components: {
    TheSettingsDialog: () => import('@/components/TheSettingsDialog.vue'),
  },

  computed: {
    ...mapState([
      'isLeftSidebarOpen',
      'version',
      'repositoryUrl',
      'discordUrl',
    ]),

    ...mapGetters([
      'GET_RELEASE_URL',
    ]),

    ...mapGetters('plex', [
      'GET_PLEX_USER',
    ]),
  },

  methods: {
    ...mapMutations([
      'SET_LEFT_SIDEBAR_OPEN',
    ]),
  },
};
</script>
