<template>
  <ion-app>
    <ion-split-pane content-id="main-content">
      <ion-menu content-id="main-content" type="overlay">
        <ion-content>
          <ion-list>
            <ion-item lines="none">
              <ion-avatar slot="start">
                <img alt="Silhouette of a person's head" src="https://ionicframework.com/docs/img/demos/avatar.svg" />
              </ion-avatar>
              <CrownIcon />
              <ion-label slot="end">
                0 Points
                <ion-icon aria-hidden="true" slot="end" :ios="chevronForwardCircleOutline" :md="chevronForwardSharp"
                  color="primary" style="margin-left: 8px;"></ion-icon>
              </ion-label>
            </ion-item>
          </ion-list>
          <ion-list id="app-list">
            <ion-list-header>Chou Tzuyu</ion-list-header>
            <ion-note>+63 912 345 6789</ion-note>

            <ion-menu-toggle :auto-hide="false" v-for="(p, i) in appPages" :key="i">
              <ion-item @click="selectedIndex = i" router-direction="root" :router-link="p.url" lines="none"
                :detail="false" class="hydrated" :class="{ selected: selectedIndex === i }">
                <ion-icon aria-hidden="true" slot="start" :ios="p.iosIcon" :md="p.mdIcon"></ion-icon>
                <ion-label>{{ p.title }}</ion-label>
                <ion-badge slot="end">{{ p.badge }}</ion-badge>
              </ion-item>
            </ion-menu-toggle>
          </ion-list>

          <ion-list id="settings-list">
            <ion-item v-for="(s, index) in settings" lines="none" :key="index">
              <ion-badge slot="end">{{ s.badge }}</ion-badge>
              <ion-icon aria-hidden="true" slot="start" :ios="s.iosIcon" :md="s.mdIcon"></ion-icon>
              <ion-label>{{ s.title }}</ion-label>
            </ion-item>
          </ion-list>
          <ion-list>
            <ion-button>Logout</ion-button>
          </ion-list>
        </ion-content>
      </ion-menu>
      <ion-router-outlet id="main-content"></ion-router-outlet>
    </ion-split-pane>
  </ion-app>
</template>

<script setup lang="ts">

import CrownIcon from './components/icons/CrownIcon.vue';
import {
  IonApp,

  IonContent,
  IonAvatar,
  IonIcon,
  IonItem,
  IonLabel,
  IonList,
  IonListHeader,
  IonMenu,
  IonMenuToggle,
  IonNote,
  IonRouterOutlet,
  IonSplitPane,
  IonButton,
} from '@ionic/vue';
import { ref } from 'vue';
import {
  archiveOutline,
  archiveSharp,
  bagCheckOutline,
  bagCheckSharp,
  bagHandleOutline,
  bagHandleSharp,
  bookmarkOutline,
  bookmarkSharp,
  caretForwardOutline,
  caretForwardSharp,
  chevronForwardCircleOutline,
  chevronForwardSharp,
  heartOutline,
  heartSharp,
  helpCircleOutline,
  helpCircleSharp,
  homeOutline,
  homeSharp,
  locationOutline,
  locationSharp,
  mailOutline,
  mailSharp,
  notificationsOutline,
  notificationsSharp,
  paperPlaneOutline,
  paperPlaneSharp,
  personOutline,
  personSharp,
  storefrontOutline,
  storefrontSharp,
  trashOutline,
  trashSharp,
  warningOutline,
  warningSharp,
} from 'ionicons/icons';

const selectedIndex = ref(0);
const appPages = [
  {
    title: 'Home',
    url: '/app/Home',
    iosIcon: homeOutline,
    mdIcon: homeSharp,
  },
  {
    title: 'Order Now',
    url: '/app/Order',
    iosIcon: bagCheckOutline,
    mdIcon: bagCheckSharp,
  },
  {
    title: 'Notifications',
    url: '/app/Notifications',
    badge: '4',
    iosIcon: notificationsOutline,
    mdIcon: notificationsSharp,
  },
  {
    title: 'Store Locator',
    url: '/app/store-locator',
    iosIcon: storefrontOutline,
    mdIcon: storefrontSharp,
  },
  {
    title: 'FAQs',
    url: '/app/frequently-asked-questions',
    iosIcon: helpCircleOutline,
    mdIcon: helpCircleSharp,
  },
];
const settings = [
  {
    title: 'My Orders',
    badge: '6',
    iosIcon: bagHandleOutline,
    mdIcon: bagHandleSharp,
  },
  {
    title: 'My Account',
    iosIcon: personOutline,
    mdIcon: personSharp,
  },
  {
    title: 'My Favorites',
    iosIcon: heartOutline,
    mdIcon: heartSharp,
  },
  {
    title: 'Order Tracker',
    iosIcon: locationOutline,
    mdIcon: locationSharp,
  },
  {
    title: 'Order History',
    iosIcon: archiveOutline,
    mdIcon: archiveSharp,
  },
]
const path = window.location.pathname.split('app/')[1];
if (path !== undefined) {
  selectedIndex.value = appPages.findIndex((page) => page.title.toLowerCase() === path.toLowerCase());
}
</script>

<style scoped>
ion-menu ion-content {
  --background: var(--ion-item-background, var(--ion-background-color, #fff));
}

#user-header {
  display: flex;
  align-items: center;
  justify-content: space-evenly;
  margin: auto;
}

#user-info {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 30px;
}

ion-menu.md ion-content {
  --padding-start: 8px;
  --padding-end: 8px;
  --padding-top: 20px;
  --padding-bottom: 20px;
}

ion-menu.md ion-list {
  padding: 20px 0;
}

ion-badge {
  background: #EDBE4C;
}

ion-button {
  margin: 20px 10px;
  width: calc(100% - 120px);
  height: 45px;
}


ion-menu.md ion-note {
  margin-bottom: 30px;
}

ion-menu.md ion-list-header,
ion-menu.md ion-note {
  padding-left: 10px;
}

ion-menu.md ion-list#app-list {
  border-bottom: 1px solid var(--ion-color-step-150, #d7d8da);
}

ion-menu.md ion-list#app-list ion-list-header {
  font-size: 22px;
  font-weight: 600;

  min-height: 20px;
}

ion-menu.md ion-list#labels-list ion-list-header {
  font-size: 16px;

  margin-bottom: 18px;

  color: #757575;

  min-height: 26px;
}

ion-menu.md ion-item {
  --padding-start: 10px;
  --padding-end: 10px;
  border-radius: 4px;
}

ion-menu.md ion-item.selected {
  --background: rgba(var(--ion-color-primary-rgb), 0.14);
}

ion-menu.md ion-item.selected ion-icon {
  color: var(--ion-color-primary);
}

ion-menu.md ion-item ion-icon {
  color: #616e7e;
}

ion-menu.md ion-item ion-label {
  font-weight: 600;
}

ion-menu.ios ion-content {
  --padding-bottom: 20px;
}

ion-menu.ios ion-list {
  padding: 20px 0 0 0;
}

ion-menu.ios ion-note {
  line-height: 24px;
  margin-bottom: 20px;
}

ion-menu.ios ion-item {
  --padding-start: 16px;
  --padding-end: 16px;
  --min-height: 50px;
}

ion-menu.ios ion-item.selected ion-icon {
  color: var(--ion-color-primary);
}

ion-menu.ios ion-item ion-icon {
  font-size: 24px;
  color: #73849a;
}

ion-menu.ios ion-list#labels-list ion-list-header {
  margin-bottom: 8px;
}

ion-menu.ios ion-list-header,
ion-menu.ios ion-note {
  padding-left: 16px;
  padding-right: 16px;
}

ion-menu.ios ion-note {
  margin-bottom: 8px;
}

ion-note {
  display: inline-block;
  font-size: 16px;

  color: var(--ion-color-medium-shade);
}

ion-item.selected {
  --color: var(--ion-color-primary);
}
</style>
