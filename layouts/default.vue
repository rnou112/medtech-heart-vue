<template>
  <v-app dark>
    <v-container class="pa-0" fluid>
      <v-row class="d-flex" align="start" no-gutters>
        <v-col cols="12" md="5" lg="4" xs="6">
          <v-container class="pa-0" :class="$vuetify.breakpoint.mdAndUp?'full-height':''">
            <v-row class="d-flex flex-column" no-gutters>
              <v-col ref="panel">
                <v-card 
                  class="pa-0 overflow-y-auto" 
                  outlined tile  
                  :class="$vuetify.breakpoint.mdAndUp?'panel-height'+multiplier:''" 
                >
                  <left-pane :panel-height="panelHeight"/>          
                </v-card>
              </v-col>
              <v-col class="d-none d-md-block fix-it">
                <navigation/>
              </v-col>
            </v-row>
          </v-container>
        </v-col>
        <v-col cols="12" md="7" lg="8" xs="6">
          <v-main>
            <v-container class="pa-0 black overflow-y-auto" :class="$vuetify.breakpoint.mdAndUp?'full-height':''">
              <Nuxt/>
            </v-container>
          </v-main>
        </v-col>
      </v-row>
      <v-row class="d-md-none" no-gutters>
        <v-col>
          <navigation/>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>

export default {
  name: 'DefaultLayout',

  data: () => {
    return {
      multiplier:1,
      panelHeight:''
    }
  },

  mounted(){
    this.panelHeight=this.$refs.panel.clientHeight
  },

  updated(){
    this.panelHeight=this.$refs.panel.clientHeight
  },

  created() {
    this.$nuxt.$on('menu-height-changed',(multiplier)=>{
      this.multiplier=multiplier
    })
  },

  beforeDestroy(){
    this.$nuxt.$off('menu-height-changed')
  }
}

</script>

<style scoped lang="scss">
  .fix-it{
    position: -webkit-sticky; /* Safari */
    position: sticky;
    bottom: 0;
  }

</style>