<template>
  <q-layout view="lHh Lpr lFf">
    <q-header >
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          color="white"
          @click="toggleLeftDrawer"
        />
        <div class="q-px-lg q-pt-xl q-mb-md">
          <div class="text-h4">Todo App</div>
          <div class="subtext-h3">{{ formattedDate }}</div>
        </div>
        <q-img
        src="../assets/mountains.png"
        class="header-image absolute-top"/>
      </q-toolbar>
    </q-header>

    <q-drawer
        v-model="leftDrawerOpen"
        show-if-above
        :width="200"
        :breakpoint="400"
      >
        <q-scroll-area style="height: calc(100% - 150px); margin-top: 150px; border-right: 1px solid #ddd">
          <q-list padding>
            <q-item
            to="/"
            exact
            clickable
            v-ripple>
              <q-item-section avatar>
                <q-icon name="list" />
              </q-item-section>

              <q-item-section>
                To Do
              </q-item-section>
            </q-item>
          </q-list>

          <q-list padding>
            <q-item
                to="/help"
                exact
                clickable
                v-ripple>
              <q-item-section avatar>
                <q-icon name="help" />
              </q-item-section>

              <q-item-section>
                Help
              </q-item-section>
            </q-item>
          </q-list>
        </q-scroll-area>

        <q-img class="absolute-top" src="../assets/mountains.png" style="height: 125px">
          <div class="absolute-bottom bg-transparent">
            <q-avatar size="56px" class="q-mb-sm">
              <img src="../assets/lorem-face-2853.jpg">
            </q-avatar>
            <div class="text-weight-bold">Georgio Kagwe</div>
            <div>@Kagweitis</div>
          </div>
        </q-img>
      </q-drawer>

      <!-- <keep-alive>
        <router-view />
      </keep-alive> -->
    <q-page-container>
      <router-view v-slot="{ Component }">
          <keep-alive>
            <component :is="Component" />
          </keep-alive>
      </router-view>
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from 'vue'
import EssentialLink from 'components/EssentialLink.vue'


export default defineComponent({
  name: 'MainLayout',

  components: {
    EssentialLink
  },


  setup () {
    const leftDrawerOpen = ref(false)
    let currentDate = new Date();
    let options = { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' };
    let formattedDate = currentDate.toLocaleDateString('en-US', options);

    return {
      leftDrawerOpen,
      formattedDate,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      }
    }
  }
})
</script>

<style lang="scss">

.header-image{
  height: 100%;
  z-index: -1;

}

</style>
