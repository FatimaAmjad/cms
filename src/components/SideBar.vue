<template>
  <div
      id="demo"
      :class="[{'collapsed' : collapsed}, {'onmobile' : isOnMobile}]"
  >
    <NavBar></NavBar>

    <div class="demo">
      <div class="container">
        <router-view />
      </div>
      <sidebar-menu
          :menu="menu"
          :collapsed="collapsed"
          :theme="selectedTheme"
          :show-one-child="true"
          @toggle-collapse="onToggleCollapse"
          @item-click="onItemClick"
      >
      </sidebar-menu>
      <div
          v-if="isOnMobile && !collapsed"
          class="sidebar-overlay"
          @click="collapsed = true"
      />
    </div>
  </div>
</template>

<script>
const separator = {
  template: `<hr style="border-color: rgba(0, 0, 0, 0.1); margin: 20px;">`
}
import NavBar from "@/components/NavBar.vue";
export default {
  name: 'SideBar',
  components: {
    NavBar,
  },
  data () {
    return {
      menu: [
        {
          header: true,
          title: 'Getting Started',
          hiddenOnCollapse: true,
        },
        {
          href: '/profile',
          title: 'Profile',
          icon:  "fas fa-id-badge"
        },
        {
          href: '/attendance',
          title: 'Attendance',
          icon:  "fas fa-clipboard-check"
        },
        {
          href: '/attendance-record',
          title: 'Attendance Record',
          icon:  "fas fa-id-badge"
        },
        {
          href: '/meeting-record',
          title: 'Meeting Record',
          icon:  "fas fa-id-badge"
        },
        {
          href: '/warnings',
          title: 'Warnings',
          icon:  "fas fa-file-alt"
        },
        {
          href: '/logs',
          title: 'Logs',
          icon:  "fas fa-file-alt"
        },
        {
          href: '/apply-for-leave',
          title: 'Apply for Leave',
          icon:  "fas fa-calendar-times"
        },
        {
          component: separator
        },
        {
          title: 'Multiple Level',
          icon: 'fa fa-list-alt',
          child: [
            {
              title: 'page'
            },
            {
              title: 'Level 2 ',
              child: [
                {
                  title: 'page'
                },
                {
                  title: 'Page'
                }
              ]
            },
            {
              title: 'Page'
            },
            {
              title: 'Another Level 2',
              child: [
                {
                  title: 'Level 3',
                  child: [
                    {
                      title: 'Page'
                    },
                    {
                      title: 'Page'
                    }
                  ]
                }
              ]
            }
          ]
        }
      ],
      collapsed: false,
      themes: [
        {
          name: 'Default theme',
          input: ''
        },
        {
          name: 'White theme',
          input: 'default-theme'
        }
      ],
      selectedTheme: 'default-theme',
      isOnMobile: false
    }
  },
  mounted () {
    this.onResize()
    window.addEventListener('resize', this.onResize)
  },
  methods: {
    onToggleCollapse (collapsed) {
      console.log(collapsed)
      this.collapsed = collapsed
    },
    // onItemClick (event, item, node) {
    //   console.log('onItemClick')
    //   console.log(event)
    //   console.log(item)
    //   console.log(node)
    // },
    onResize () {
      if (window.innerWidth <= 767) {
        this.isOnMobile = true
        this.collapsed = true
      } else {
        this.isOnMobile = false
        this.collapsed = false
      }
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Source+Sans+Pro:400,600');
body,
html {
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Source Sans Pro', sans-serif;
  font-size: 18px;
  background-color: #f2f4f7;
  color: #262626;
}
#demo {
  padding-left: 350px;
  transition: 0.3s ease;
}
#demo.collapsed {
  padding-left: 50px;
}
#demo.onmobile {
  padding-left: 50px;
}
.sidebar-overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background-color: #000;
  opacity: 0.5;
  z-index: 900;
}
.demo {
  padding: 50px;
}
.container {
  max-width: 900px;
}
pre {
  font-family: Consolas, monospace;
  color: #000;
  background: #fff;
  border-radius: 2px;
  padding: 15px;
  line-height: 1.5;
  overflow: auto;
}
</style>