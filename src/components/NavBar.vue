<template>
  <header class="nav-bar " ref="navBar">
    <div>
      <figure>
        <img
            @click="goToHome"
            src="../assets/BaseIcons/logo.png"
            alt="logo">
      </figure>
      <HamburgerMenu
          :isOpen="isOpen"
          @action="handleHambMenu"/>
    </div>
      <nav>
        <router-link v-for="item in links"
                     :key="item.id"
                     :to="item.path">
                      <span @click="HandleChangeRoute">{{item.name}}</span>          
        </router-link>
        <button v-if="!isLogged" @click="goToLogin">Login</button>
        <button v-else @click="handleLogout"> Logout</button>
      </nav>
  </header>
</template>

<script>
  import HamburgerMenu from "./HamburgerMenu.vue";
      export default {
        name: "NavBar",
        components: {HamburgerMenu},
        data(){
        return{
          links: [
            {
              path:'/calculator',
              name:'Calculator'
            },
            {
              path:'/mathquiz',
              name:'Math Quizz',
            },
            {
              path:'/todolist',
              name: 'To Do List'
            },
          ],
          isOpen: false,
        }
      },

        computed: {
          isLogged() {
            return this.$store.state.auth.isLogged
          }
        },

        methods: {
        handleHambMenu() {
          this.isOpen = !this.isOpen
        this.$refs.navBar.style.height = this.isOpen ? '100%' : '60px'
        },
        HandleChangeRoute() {
        this.isOpen = false
        this.$refs.navBar.style.height = '60px'
        },
        goToHome() {
          this.isOpen = false
          this.$refs.navBar.style.height = '60px'
          return this.$router.push('/')
        },
        goToLogin() {
          this.isOpen = false
          this.$refs.navBar.style.height = '60px'
          return this.$router.push('/login')
        },
        handleLogout() {
          this.$store.dispatch('logout')
          console.log(this.isLogged)
        },
      }
    }
</script>

<style lang="scss">
  @import '../styles/vars.scss';

  @media only screen and (min-width: 0) {
    .nav-bar {
      font-family: Helvetica, sans-serif;
      height: 60px;
      top: 0;
      left: 0;
      overflow: hidden;
      transition: height 0.3s ease-in-out;
      align-items: center;
      z-index: 99;
      position: fixed;
      width: 100%;
      background-color: white;
      > div {
        padding: 0 16px 24px 0;
        display: flex;
        justify-content: space-between;
        align-items: center;
      }
      nav {
        margin-top: 120px;
        text-align: center;
      }
      a {
        margin: 30px 0;
        display: block;
        text-decoration: none;
        color: rgba($color: #000000, $alpha: 1.0);
        font-size: 18px;
      }
      img {
        cursor: pointer;
        width: 60px;
      }
      button {
        font-size: 16px;
        font-weight: bold;
        color: white;
        background-color: $light-blue;
        padding: 7px 35px;
        border-radius: 33px;
        border: none;
        cursor: pointer;
      }
    }
}
  @media only screen and (min-width: 768px) {
    .nav-bar {
      width: 100%;
      display: flex;
      justify-content: space-between;
      align-items: center;
      img {
        padding-top: 30px;
      }
      nav {
        margin: 0 30px 0;

        a {
          margin: 0 12px;
          display: inline-block;
          color: $dark-blue;
          transition: transform .1s;
          &:hover {
            transform: scale(1.06);
            color: $light-blue;
          }
          &:nth-child(3) {
            margin-right: 20px;
          }
        }
        button {
          color: white;
          background-color: $light-blue;
          padding: 7px 20px;
          border-radius: 33px;
          border: none;
          cursor: pointer;
          transition: transform 0.2s;
          &hover {
            transform: scale(1.1);
          }
        }
      }
    }
  }
</style>
