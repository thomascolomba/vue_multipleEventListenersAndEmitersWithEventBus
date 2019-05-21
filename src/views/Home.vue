<template>
  <div class="home">
    <div class="comps">
      <Comp1/>
      <Comp2/>
      <Comp3/>
      <Comp4/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Comp1 from '@/components/Comp1.vue'
import Comp2 from '@/components/Comp2.vue'
import Comp3 from '@/components/Comp3.vue'
import Comp4 from '@/components/Comp4.vue'
export default {
  name: 'home',
  components: {
    Comp1,
    Comp2,
    Comp3,
    Comp4
  }
}
</script>
<style>
.comps {
  width:600px;
  height:600px;
  margin-left:auto;
  margin-right:auto;
  color:black;
}
</style>
