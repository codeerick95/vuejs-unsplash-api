<template>
  <div class="card border-0">
    <img :src="photo.urls.regular" alt="Demo" class="img-fluid" />
    <div
      class="card-img-overlay d-flex justify-content-between align-items-start"
    >
      <template v-if="photo">
        <div>
          <img
            :src="photo.user.profile_image.small"
            alt="User profile image"
            class="rounded-circle"
          />
          <a href class="btn btn-link text-white">{{ photo.user.username }}</a>
        </div>
        <span class="badge badge-light align-self-end">
          <img src="../assets/like.png" alt="Icon like" class="icon" />
          {{ photo.likes }}
        </span>
      </template>
    </div>
  </div>
</template>

<script>
export default {
  props: ["photo"]
};
</script>

<style scoped></style>
