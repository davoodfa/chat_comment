<template>
  <v-card
    class="mx-auto mt-2"
    color="#c66bfc"
    theme="dark"
    max-width="400">
    <v-card-text>
      <v-row>
        <v-col cols="12">
          <v-text-field
            append-icon="mdi-send"
            append-inner-icon="mdi-map-marker"
            prepend-icon="mdi-account"
            variant="filled"
            clear-icon="mdi-close-circle"
            clearable
            label="Start a Discussion"
            type="text"
          ></v-text-field>
        </v-col>
      </v-row>
    </v-card-text>
    <v-card
      class="mx-auto mb-1"
      color="#26c6da"
      theme="dark"
      max-width="400"
      v-for="item in comments" :key="item.id">
      <v-card-actions>
        <v-list-item class="w-100">
          <template v-slot:title>
            <div class="d-flex flex-row mb-2 ">
              <v-avatar
                color="grey-darken-3"
                :image="item.user.avatar"
              ></v-avatar>
              <v-list-item-title class="ml-2 mt-1">{{ item.user.name }}</v-list-item-title>
            </div>
          </template>
          <v-card-text class="text-h6 py-2">
            {{ item.text }}
          </v-card-text>
          <div class="">
            <v-btn>
              <v-icon v-if="item.iLikedIt" class="me-1" icon="mdi-thumb-up-outline"></v-icon>
              <v-icon v-else class="me-1" icon="mdi-thumb-up"></v-icon>
              {{ item.likes }}
            </v-btn>
            <v-btn variant="text" @click="showReplay(item.id)">Replay</v-btn>
            <v-text-field v-if="item.replayVisible" clearable label="Replay"></v-text-field>
          </div>
          <v-card
            class="mx-auto mb-1"
            color="#111"
            theme="dark"
            max-width="400"
            v-show="item.replies.length > 0" v-for="rep in item.replies" :key="rep.id">
            <v-card-actions>
              <v-list-item class="w-100">
                <template v-slot:title>
                  <div class="d-flex flex-row mb-2 ">
                    <v-avatar
                      color="grey-darken-3"
                      :image="rep.user.avatar"
                    ></v-avatar>
                    <v-list-item-title class="ml-2 mt-1">{{ rep.user.name }}</v-list-item-title>
                  </div>
                </template>
                <v-card-text class="text-h6 py-2">
                  {{ rep.text }}
                </v-card-text>
                <div class="">
                  <v-btn>
                    <v-icon v-if="rep.iLikedIt" class="me-1" icon="mdi-thumb-up-outline"></v-icon>
                    <v-icon v-else class="me-1" icon="mdi-thumb-up"></v-icon>
                    {{ rep.likes }}
                  </v-btn>
                </div>
              </v-list-item>
            </v-card-actions>
          </v-card>

        </v-list-item>
      </v-card-actions>
    </v-card>
  </v-card>
</template>

<script>
import {discussions} from "@/data/discussions";

export default {
  name: "Comments.vue",
  data: () => ({
    comments: discussions
  }),
  methods: {
    showReplay(id) {
      this.comments.map(c => {
        if (c.id == id) {
          c.replayVisible = !c.replayVisible
        }
      })
    }
  },
  computed: {},
  mounted() {
    console.log('mounted')
  }
}
</script>

<style scoped>

</style>
