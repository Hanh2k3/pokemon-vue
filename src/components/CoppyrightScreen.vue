<template>
  <div class="screen">
    <p class="copyright">
      This game owned by Hạnh handsome when learn Vue 3 course for begginers -
      <a href="https://www.facebook.com/profile.php?id=100048447487944">
        Contact Here
      </a>
    </p>
  </div>
</template>

<style lang="css" scoped>
.copyright {
  position: fixed;
  left: 50%;
  transform: translateX(-50%);
  bottom: 1.5rem;
  color: var(--light);
  z-index: 3;
  font-size: 1.5rem;
}
.copyright a {
  color: #f4dc26;
}
</style>
