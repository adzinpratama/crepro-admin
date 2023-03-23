<template>
  <nav>
    <div class="logo-name">
      <div class="logo-image">
        <img src="../assets/Images/logo.png" alt="" />
      </div>
      <div class="logo_name">Bs Admin</div>
    </div>
    <div class="menu-items">
      <ul class="nav-links" v-on:scroll="handleScroll">
        <li>
          <div
            class="iocn-link"
            :class="[{ active: toggleMenu }]"
            @click="() => (toggleMenu = !toggleMenu)"
          >
            <a href="#">
              <i class="uil uil-estate"></i>
              <span class="link-name">Dahsboard</span>
            </a>
            <i class="uil uil-angle-right-b rotate"></i>
          </div>
          <ul :class="['dropdown-menu', { show: toggleMenu }]">
            <li>
              <a href="#">
                <sapn class="link-name">Dashboard V1</sapn>
              </a>
            </li>
            <li>
              <a href="#">
                <sapn class="link-name">Dashboard V1</sapn>
              </a>
            </li>
            <li>
              <a href="#">
                <sapn class="link-name">Dashboard V1</sapn>
              </a>
            </li>
          </ul>
        </li>
        <li>
          <a href="#">
            <i class="uil uil-files-landscapes"></i>
            <span class="link-name">Content</span>
          </a>
        </li>
        <li>
          <a href="#">
            <i class="uil uil-chart"></i>
            <span class="link-name">Analytics</span>
          </a>
        </li>
        <li>
          <a href="#">
            <i class="uil uil-thumbs-up"></i>
            <span class="link-name">Like</span>
          </a>
        </li>
        <li>
          <a href="#">
            <i class="uil uil-comments"></i>
            <span class="link-name">Comment</span>
          </a>
        </li>
        <li v-for="i in 15" :key="i">
          <a href="#">
            <i class="uil uil-share"></i>
            <span class="link-name">Share</span>
          </a>
        </li>
      </ul>

      <ul class="logout-mode">
        <li>
          <a href="#">
            <i class="uil uil-signout"></i>
            <span class="link-name">Logout</span>
          </a>
        </li>

        <li class="mode">
          <a href="#">
            <i class="uil uil-moon"></i>
            <span class="link-name">Dark Mode</span>
          </a>

          <div class="mode-toggle" @click="toggleMode">
            <span class="switch"></span>
          </div>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { handleError, onMounted, ref } from "@vue/runtime-core";

const toggleMenu = ref(true);

const toggleMode = () => {
  let body = document.body.classList;
  body.toggle("dark");
  if (body.contains("dark")) localStorage.setItem("mode", "dark");
  else localStorage.setItem("mode", "light");
};

const handleScroll = (e) => {
  e.target.classList.add("scroll");
  setTimeout(() => {
    e.target.classList.remove("scroll");
  }, 2000);
};

onMounted(() => {
  let getMode = localStorage.getItem("mode");
  if (getMode && getMode == "dark") document.body.classList.toggle("dark");
});
</script>

<style lang="scss">
nav {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 250px;
  padding: 10px 14px;
  background-color: var(--panel-color);
  border-right: 1px solid var(--border-color);
  transition: var(--tran-05);

  &.close {
    width: 73px;

    .logo_name {
      opacity: 0;
      pointer-events: none;
    }
  }

  .logo-name {
    display: flex;
    align-items: center;
  }

  .logo-image {
    display: flex;
    justify-content: center;
    min-width: 45px;
  }

  .logo-image img {
    width: 40px;
    object-fit: cover;
    border-radius: 50%;
  }

  .logo-name .logo_name {
    font-size: 22px;
    font-weight: 600;
    color: var(--text-color);
    margin-left: 14px;
    transition: var(--tran-05);
  }

  .menu-items {
    margin-top: 40px;
    height: calc(100% - 90px);
    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }

  .nav-links {
    overflow-y: auto;
    overflow-x: hidden;

    &::-webkit-scrollbar {
      display: none;
      width: 3px;
    }

    &.scroll {
      &::-webkit-scrollbar {
        display: block;
      }
    }
  }
}

.menu-items li {
  list-style: none;
}

.menu-items li a {
  display: flex;
  align-items: center;
  height: 50px;
  text-decoration: none;
  position: relative;
}

.nav-links li a:hover:before {
  content: "";
  position: absolute;
  left: -7px;
  height: 2rem;
  width: 5px;
  border-radius: 10px;
  background-color: var(--primary-color);
}

.nav-links li i {
  transition: var(--tran-05);
}

.nav-links li .iocn-link {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.nav-links li .active i.rotate {
  transform: rotate(90deg);
}

nav.close .nav-links li .iocn-link i.rotate {
  display: none;
}

nav.close .nav-links li .dropdown-menu {
  position: absolute;
  left: 110%;
  top: -10px;
  margin-top: 0;
  padding: 10px 20px;
  // border-radius: 0 6px 6px 0;
  // opacity: 0;
  display: block;
  pointer-events: none;
  transition: 0s;
}

nav.close .nav-links li a:hover {
  .dropdown-menu {
    left: -100%;
    top: 0;
    transition: all 0.4s ease;
  }
}

.dropdown-menu {
  display: none;
  transition: var(--tran-05);
  background: var(--toggle-color);
  // padding: 10px;
  width: 100%;
  border-radius: 10px;

  a:before {
    display: none;
  }

  &.show {
    display: inline-block;
  }

  padding-left: 45px;
}

body.dark li a:hover:before {
  background-color: var(--text-color);
}

.menu-items li a i,
.menu-items li i {
  font-size: 24px;
  min-width: 45px;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--black-light-color);
}

.menu-items li a .link-name {
  font-size: 18px;
  font-weight: 400;
  color: var(--black-light-color);
  transition: var(--tran-05);
}

nav.close li a .link-name {
  opacity: 0;
  pointer-events: none;
}

.nav-links li a:hover i,
.nav-links li a:hover .link-name {
  color: var(--primary-color);
}

body.dark .nav-links li a:hover i,
body.dark .nav-links li a:hover .link-name {
  color: var(--text-color);
}

.menu-items .logout-mode {
  padding-top: 10px;
  border-top: 1px solid var(--border-color);
}

.menu-items .mode {
  display: flex;
  align-items: center;
  white-space: nowrap;
}

.menu-items .mode-toggle {
  position: absolute;
  right: 14px;
  height: 50px;
  min-width: 45px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}

.mode-toggle .switch {
  position: relative;
  display: inline-block;
  height: 22px;
  width: 40px;
  border-radius: 25px;
  background-color: var(--toggle-color);
}

.switch:before {
  content: "";
  position: absolute;
  left: 5px;
  top: 50%;
  transform: translateY(-50%);
  height: 15px;
  width: 15px;
  background-color: var(--panel-color);
  border-radius: 50%;
  transition: var(--tran-03);
}

body.dark .switch:before {
  left: 20px;
}
</style>
