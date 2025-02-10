<template>
  <nav class="navbar">
    <div class="container container-navbar">
      <div class="navbar-left">
        <img
          src="@/assets/crypto-icon.png"
          alt="Crypto Logo"
          class="logo-img"
        />
        <ul class="nav-links">
          <li><a href="#">Pasar</a></li>
          <li><a href="#">Tentang Kami</a></li>
          <li><a href="#">Kontak Kami</a></li>
        </ul>
      </div>
      <div class="auth-buttons">
        <button class="signin">SIGN IN</button>
        <button class="signup">SIGN UP</button>
      </div>
      <button class="menu-button" @click="toggleMenu">
        <svg
          v-if="!isMenuOpen"
          class="w-6 h-6"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h16m-16 6h16"
          />
        </svg>
        <svg v-else class="w-6 h-6" viewBox="0 0 24 24" stroke="currentColor">
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M6 18L18 6M6 6l12 12"
          />
        </svg>
      </button>
    </div>
    <div v-if="isMenuOpen" class="mobile-menu">
      <a href="#">Pasar</a>
      <a href="#">Tentang Kami</a>
      <a href="#">Kontak Kami</a>
      <button class="signin">SIGN IN</button>
      <button class="signup">SIGN UP</button>
    </div>
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
    },
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
  height: 80px; /* Ensuring the navbar has enough height */
}

.container-navbar {
  display: flex;
  justify-content: space-between;
  width: 100%;
}

/* Navbar Left Section */
.navbar-left {
  display: flex;
  align-items: center;
  gap: 20px; /* Adds spacing between the logo and links */
}

/* Logo */
.logo-img {
  height: 50px;
  width: auto;
  margin-right: 15px;
  display: block;
}

/* Navigation Links */
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
  font-size: 16px;
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
  border: 1px solid #d57c17;
  color: #d57c17;
  padding: 0.5rem 1rem;
  border-radius: 100px;
  transition: background 0.3s ease;
  font-size: 14px;
  background: transparent;
}

.auth-buttons button:hover {
  background: white;
  color: black;
}

/* Mobile Menu Button - Only Visible on Mobile */
.menu-button {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  padding: 10px;
}

/* Mobile Menu Styling */
@media (max-width: 768px) {
  .nav-links,
  .auth-buttons {
    display: none;
  }

  .menu-button {
    display: block;
    position: absolute;
    right: 15px;
    top: 50%;
    transform: translateY(-50%);
    z-index: 100;
  }

  .mobile-menu {
    background: black;
    position: absolute;
    top: 65px;
    left: 50%;
    transform: translateX(-50%);
    width: 90%;
    max-width: 300px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 15px;
    padding: 1.5rem;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(255, 223, 0, 0.3);
    z-index: 99;
  }

  .mobile-menu a {
    color: white;
    font-size: 18px;
    font-weight: 500;
    padding: 10px;
    text-decoration: none;
  }

  .mobile-menu button {
    width: 100%;
    max-width: 250px;
    padding: 12px;
    border-radius: 8px;
    border: 1px solid yellow;
    color: yellow;
    font-size: 16px;
    text-align: center;
    background: transparent;
    transition: background 0.3s ease, color 0.3s ease;
  }

  .mobile-menu button:hover {
    background: yellow;
    color: black;
  }
}
</style>
