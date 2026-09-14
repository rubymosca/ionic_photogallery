<template>
  <div class="custom-card">
    <div class="gallery-header">
      <h2 class="card-title">Your Gallery</h2>
      <span class="badge">{{ photos.length }} {{ photos.length === 1 ? 'Photo' : 'Photos' }}</span>
    </div>

    <!-- Empty State -->
    <div v-if="photos.length === 0" class="empty-gallery">
      <div class="empty-icon">
        <ion-icon :icon="imagesOutline" />
      </div>
      <p class="empty-title">No pictures yet</p>
      <p class="empty-sub">Take a photo above to add it to your collection.</p>
    </div>

    <!-- Grid View -->
    <div v-else class="image-grid">
      <div
        v-for="(photo, index) in photos"
        :key="index"
        class="image-item"
      >
        <img :src="photo" alt="Captured Photo" loading="lazy" />
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { IonIcon } from "@ionic/vue";
import { imagesOutline } from "ionicons/icons";

defineProps<{ photos: string[] }>();
</script>

<style scoped>
.custom-card {
  background: #ffffff;
  border-radius: 20px;
  padding: 20px;
  box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.05), 0 8px 10px -6px rgba(0, 0, 0, 0.01);
  border: 1px solid #f1f5f9;
}

.gallery-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 16px;
}

.card-title {
  margin: 0;
  font-size: 1.1rem;
  font-weight: 700;
  color: #0f172a;
}

.badge {
  background: #f1f5f9;
  color: #475569;
  font-size: 0.75rem;
  font-weight: 600;
  padding: 4px 10px;
  border-radius: 20px;
}

.empty-gallery {
  text-align: center;
  padding: 36px 16px;
}

.empty-icon {
  font-size: 2.5rem;
  color: #cbd5e1;
  margin-bottom: 8px;
}

.empty-title {
  margin: 0;
  font-size: 0.95rem;
  font-weight: 600;
  color: #475569;
}

.empty-sub {
  margin: 4px 0 0 0;
  font-size: 0.8rem;
  color: #94a3b8;
}

.image-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 12px;
}

@media (min-width: 480px) {
  .image-grid {
    grid-template-columns: repeat(3, 1fr);
  }
}

.image-item {
  aspect-ratio: 1 / 1;
  border-radius: 14px;
  overflow: hidden;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
  border: 1px solid #e2e8f0;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}

.image-item:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.12);
}

.image-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
</style>