# iview-area-al-cascader
<template>
    <div>
        <al-cascader
                v-model="selectRegion" @on-change="selectedRegion"
                data-type="all" size="small"
                level="3"
                placeholder="请选择区域！"
                :render-format="label => label.join('｜')"
        />
    </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';
  import iviewArea from 'iview-area';

  Vue.use(iviewArea);

  /* 区域选择 */
  export default {
    name: 'region-base',
    props: {
      selectRegions: {
        type: Array,
        default: []
      }
    },
    data () {
      return {
        region: {provinceId: '', cityId: '', countyId: '', townsId: '', addess: '', addressCode: []},
        selectRegion: []
      };
    },
    methods: {
      selectedRegion (region) {
        this.region.provinceId = region[0].code;
        this.region.cityId = region[1].code;
        this.region.addess = region[0].name + region[1].name;
        this.region.addressCode = [region[0].code, region[1].code];
        if(region.length===3){
          this.region.countyId = region[2].code;
          this.region.addess = region[0].name + region[1].name + region[2].name ;
          this.region.addressCode = [region[0].code, region[1].code, region[2].code];
        }if(region.length===4){
          this.region.countyId = region[2].code;
          this.region.townsId = region[3].code;
          this.region.addess = region[0].name + region[1].name + region[2].name + region[3].name;
          this.region.addressCode = [region[0].code, region[1].code, region[2].code, region[3].code];
        }
        this.$emit('selectedRegion', this.region);
      }
    },
    watch: {
      selectRegions: function (newRegion) {
        if (newRegion.length > 0) {
          this.selectRegion = newRegion;
        } else {
          this.selectRegion = [];
        }
      }
    },

  };
</script>
<style>

</style>
