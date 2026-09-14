<template>
  <ion-page>
    <!-- Header -->
    <ion-header class="ion-no-border navbar">
      <ion-toolbar class="transparent-toolbar">
        <ion-title class="brand-title">
          <div class="logo-badge">
            <ion-icon :icon="cameraOutline" />
          </div>
          <span>SnapGallery</span>
        </ion-title>
      </ion-toolbar>
    </ion-header>

    <ion-content :fullscreen="true" class="page-background">
      <div class="container">
        <!-- Hero Banner / Action Area -->
        <section class="card-wrapper">
          <CameraComponent @photoCaptured="addPhoto" />
        </section>

        <!-- Photos Section -->
        <section class="card-wrapper">
          <PhotoGalleryComponent :photos="photos" />
        </section>
      </div>
    </ion-content>
  </ion-page>
</template>

<script setup lang="ts">
import { ref } from 'vue';
import {
  IonContent,
  IonHeader,
  IonPage,
  IonTitle,
  IonToolbar,
  IonIcon,
} from '@ionic/vue';
import { cameraOutline } from 'ionicons/icons';
import CameraComponent from '@/components/CameraComponent.vue';
import PhotoGalleryComponent from '@/components/PhotoGalleryComponent.vue';

const photos = ref<string[]>([]);

const addPhoto = (photoPath: string) => {
  photos.value.unshift(photoPath);
};
</script>

<style scoped>
.page-background {
  --background: #f1f5f9;
}

.navbar {
  background: #ffffff;
  border-bottom: 1px solid #e2e8f0;
}

.transparent-toolbar {
  --background: #ffffff;
}

.brand-title {
  display: flex;
  align-items: center;
  font-weight: 800;
  font-size: 1.2rem;
  color: #0f172a;
  letter-spacing: -0.025em;
}

.logo-badge {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #3b82f6, #2563eb);
  color: #ffffff;
  width: 34px;
  height: 34px;
  border-radius: 10px;
  margin-right: 10px;
  box-shadow: 0 4px 10px rgba(37, 99, 235, 0.3);
}

.logo-badge ion-icon {
  font-size: 1.2rem;
}

.container {
  max-width: 640px;
  margin: 0 auto;
  padding: 20px 16px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.card-wrapper {
  animation: slideUp 0.3s ease-out;
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(12px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>