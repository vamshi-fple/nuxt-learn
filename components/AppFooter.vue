<template>
    <footer class="footer-container">
      <div class="footer-content">
        <div class="social-links">
          <a href="https://twitter.com" target="_blank" class="social-link">Twitter</a>
          <a href="https://facebook.com" target="_blank" class="social-link">Facebook</a>
          <a href="https://instagram.com" target="_blank" class="social-link">Instagram</a>
        </div>
        <p class="footer-text">© 2025 Your Company. All rights reserved.</p>
      </div>
    </footer>
  </template>
  
  <style scoped>
  .footer-container {
    display: flex;
    justify-content: center;
    background: #f8f9fa;
    padding: 1rem;
    border-radius: 10px;
    margin: 2rem auto 1rem auto;
    box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.05);
  }
  
  .footer-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
    max-width: 1000px;
    width: 100%;
  }
  
  .social-links {
    display: flex;
    gap: 1rem;
  }
  
  .social-link {
    color: #333;
    text-decoration: none;
    transition: color 0.2s;
  }
  
  .social-link:hover {
    color: #3b82f6;
  }
  
  .footer-text {
    font-size: 0.9rem;
    color: #666;
  }
  </style>
  