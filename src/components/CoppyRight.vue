<template>
   <div class="copyright">
        <p>CoppyRight &copy; By ThanhTai <a href="https://www.facebook.com/tai.thanh.9638/">Here</a></p>
   </div>
</template>
<script>
export default {
    
}
</script>
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