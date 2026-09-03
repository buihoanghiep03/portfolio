<template>
  <footer class="footer">
    <div class="container footer-inner">
      <p class="footer-text">
        Designed &amp; Built by <strong>Bùi Hoàng Hiệp</strong>
      </p>
      <p class="footer-year">© 2026</p>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  border-top: 1px solid var(--color-border);
  background: var(--color-bg-soft);
  padding: 32px 0;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
  gap: 12px;
}

.footer-text {
  color: var(--color-text-muted);
  font-size: 0.92rem;
}

.footer-text strong {
  color: var(--color-text);
}

.footer-year {
  color: var(--color-text-muted);
  font-size: 0.92rem;
}
</style>
