<template>
  <div class="custom-card">
    <div class="card-header">
      <div class="icon-box">
        <ion-icon :icon="cameraIcon" />
      </div>
      <div>
        <h2 class="card-title">Capture Photo</h2>
        <p class="card-subtitle">Take a quick picture using your camera</p>
      </div>
    </div>

    <div class="card-body">
      <ion-button expand="block" class="capture-btn" @click="takePicture">
        <ion-icon slot="start" :icon="cameraIcon" />
        Take Picture
      </ion-button>

      <div v-if="errorMessage" class="error-banner">
        <p>{{ errorMessage }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { IonButton, IonIcon } from "@ionic/vue";
import { camera as cameraIcon } from "ionicons/icons";
import { Camera } from "@capacitor/camera";
import { ref } from "vue";

const errorMessage = ref("");
const emit = defineEmits<{ (event: "photoCaptured", photo: string): void }>();

const takePicture = async () => {
  errorMessage.value = "";
  try {
    const photo = await Camera.takePhoto({ quality: 90, saveToGallery: false });
    if (photo.webPath) {
      emit("photoCaptured", photo.webPath);
    }
  } catch (error) {
    console.error(error);
    errorMessage.value = "Unable to capture photo.";
  }
};
</script>

<style scoped>
.custom-card {
  background: #ffffff;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.01);
  border: 1px solid #f1f5f9;
}

.card-header {
  display: flex;
  align-items: center;
  gap: 14px;
  margin-bottom: 16px;
}

.icon-box {
  width: 44px;
  height: 44px;
  border-radius: 12px;
  background: #eff6ff;
  color: #2563eb;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.4rem;
}

.card-title {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 700;
  color: #0f172a;
}

.card-subtitle {
  margin: 2px 0 0 0;
  font-size: 0.85rem;
  color: #64748b;
}

.capture-btn {
  --background: linear-gradient(135deg, #2563eb 0%, #1d4ed8 100%);
  --border-radius: 14px;
  --box-shadow: 0 6px 16px rgba(37, 99, 235, 0.35);
  --color: #ffffff;
  font-weight: 600;
  font-size: 0.95rem;
  height: 50px;
  text-transform: none;
  letter-spacing: 0.2px;
}

.error-banner {
  margin-top: 12px;
  padding: 10px 14px;
  background: #fef2f2;
  border-radius: 10px;
  border: 1px solid #fecaca;
  color: #dc2626;
  font-size: 0.85rem;
}
</style>