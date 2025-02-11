<template>
  <nav class="navbar">
    <div class="container container-navbar">
      <div class="navbar-left">
        <img
          src="@/assets/crypto-icon.png"
          alt="Crypto Logo"
          class="logo-img"
        />
        <ul :class="['nav-links', { 'nav-open': isMenuOpen }]">
          <li><a href="#">Pasar</a></li>
          <li><a href="#">Tentang Kami</a></li>
          <li><a href="#">Kontak Kami</a></li>
        </ul>
      </div>

      <!-- Authentication Buttons (Hidden on Mobile) -->
      <div class="auth-buttons">
        <button class="signin">SIGN IN</button>
        <button class="signup">SIGN UP</button>
      </div>

      <!-- Hamburger Menu Button -->
      <button class="menu-button" @click="toggleMenu">
        <svg
          v-if="!isMenuOpen"
          class="w-8 h-8"
          viewBox="0 0 24 24"
          stroke="white"
          fill="none"
          stroke-width="2"
        >
          <path d="M4 6h16M4 12h16M4 18h16" />
        </svg>
        <svg
          v-else
          class="w-8 h-8"
          viewBox="0 0 24 24"
          stroke="white"
          fill="none"
          stroke-width="2"
        >
          <path d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </div>

    <!-- Mobile Menu -->
    <div v-if="isMenuOpen" class="mobile-menu">
      <a href="#">Pasar</a>
      <a href="#">Tentang Kami</a>
      <a href="#">Kontak Kami</a>
      <button class="signin">SIGN IN</button>
      <button class="signup">SIGN UP</button>
    </div>

    <!-- Background Overlay when Mobile Menu is Open -->
    <div v-if="isMenuOpen" class="overlay" @click="toggleMenu"></div>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      isMenuOpen: false,
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
      document.body.style.overflow = this.isMenuOpen ? "hidden" : "";
    },
  },
  beforeUnmount() {
    document.body.style.overflow = "";
  },
};
</script>

<style>
/* Navbar */
.navbar {
  font-family: "Roboto", sans-serif;
  background-color: #000;
  padding: 1.2rem 2rem;
  width: 100%;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  z-index: 100;
  height: 80px;
}

/* Navbar Container */
.container-navbar {
  display: flex;
  justify-content: space-between;
  width: 100%;
  align-items: center;
}

/* Navbar Left */
.navbar-left {
  display: flex;
  align-items: center;
  gap: 20px;
}

/* Logo */
.logo-img {
  height: 50px;
  width: auto;
}

/* Desktop Nav Links */
.nav-links {
  display: flex;
  list-style: none;
  gap: 25px;
  padding: 0;
  margin: 0;
  font-size: 16px;
}

.nav-links a {
  color: white;
  text-decoration: none;
  font-weight: 500;
  transition: color 0.3s ease;
}

.nav-links a:hover {
  color: #d57c17;
}

/* Authentication Buttons */
.auth-buttons {
  display: flex;
  gap: 15px;
  align-items: center;
}

.auth-buttons button {
  border: 3px solid #d57c17;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 100px;
  transition: background 0.3s ease;
  font-weight: bold;
  font-size: 14px;
  background: transparent;
  width: 121px;
  height: 43px;
}

.auth-buttons button:hover {
  background: white;
  color: black;
}

/* Hide Auth Buttons on Mobile */
@media (max-width: 768px) {
  .auth-buttons {
    display: none;
  }
}

/* Mobile Menu Button */
.menu-button {
  width: 40px; /* Set fixed size */
  height: 40px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 5px;
  border: none;
  background: none;
  cursor: pointer;
  position: absolute;
  right: 15px; /* Align to right */
  top: 50%;
  transform: translateY(-50%);
  z-index: 110;
}

.menu-button svg {
  width: 24px; /* Set icon size */
  height: 24px;
  padding: 2rem;
}

/* Mobile Menu Styling */
@media (max-width: 768px) {
  .nav-links {
    display: none;
  }

  .menu-button {
    display: contents;
  }

  .mobile-menu {
    background: rgba(20, 20, 20, 0.95);
    position: absolute;
    top: 80px;
    left: 50%;
    transform: translateX(-50%);
    width: 85%;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
    padding: 1.5rem;
    border-radius: 12px;
    z-index: 105;
    transition: all 0.3s ease-in-out;
  }

  .mobile-menu a {
    color: white;
    font-size: 18px;
    font-weight: 500;
    text-decoration: none;
  }

  .mobile-menu button {
    width: 100%;
    max-width: 250px;
    padding: 12px;
    border-radius: 8px;
    border: 2px solid #d57c17;
    color: #d57c17;
    font-size: 16px;
    text-align: center;
    background: transparent;
    transition: background 0.3s ease, color 0.3s ease;
  }

  .mobile-menu button:hover {
    background: #facc15;
    color: white;
  }

  /* Background Overlay */
  .overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    z-index: 104;
  }
}
</style>
