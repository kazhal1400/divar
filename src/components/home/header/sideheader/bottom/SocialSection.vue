<template>
  <div class="" v-if="group_item_name == 'رویداد'">
    <roidad />
  </div>
  <div class="" v-if="group_item_name == 'داوطلبانه'">
    <davtalabane />
  </div>
  <div class="" v-if="group_item_name == 'گم شده ها'">
    <gomshodeha />
  </div>
  <cllapse-btntwo
    :price_items="social_price_items"
    :marks="social_priceMarks"
    @minp="minp"
    @maxp="maxp"
    id="social_price"
    exm="100,000"
    txt="تومان"
  />

  <hr />
  <moving-btn
    :conValue="del_tavafoghi"
    @conFn="conTavafoghiFn"
    title=" حذف توافقی ها"
  />
  <hr />
  <cllapse-btnone
    :data_items="moaveze_items"
    :marks="moavezeMarks"
    @dataFn="moavezeFn"
    id="moaveze"
    exm="نمایش معاوضه ها"
  />
</template>

<script>
import { computed, ref } from '@vue/reactivity';
import { inject } from '@vue/runtime-core';
import roidad from "./social/roidad.vue";
import davtalabane from "./social/davtalabane.vue";
import gomshodeha from "./social/gomshodeha.vue";
import CllapseBtntwo from "../UI/CllapseBtntwo.vue";
import CllapseBtnone from "../UI/CllapseBtnone.vue";
import MovingBtn from "../UI/MovingBtn.vue";
export default {
  components: {
    roidad,
    davtalabane,
    gomshodeha,
CllapseBtntwo,
    CllapseBtnone,
    MovingBtn,
  },
  setup() {
     const info = inject("info");
    const group_item_name = computed(() => info.group_item_name);
    const social_priceMarks = computed(() => info.subItem.social_price);
    const social_price_items = ref(["قیمت", "حداقل", "حداکثر"]);


    const moavezeMarks = ["نمایش فقط معاوضه ها", "حذف معاوشه ها"];
    const moaveze_items = ref("نمایش  معاوضه ها");

    const del_tavafoghi = computed(() => info.del_tavafoghi);

    function conTavafoghiFn() {
      info.del_tavafoghi = !info.del_tavafoghi;
    }
    /*
vadie_melk: "",
      ejare_melk: "",
      vadie_ejare_melk: "",
      vadie_tejari: "",
      ejare_tejari: "",
 */
    function minp(minprice) {
      info.minprice = minprice;
    }
    function maxp(maxprice) {
      info.maxprice = maxprice;
    }

   
    
    function moavezeFn(moaveze) {
      info.moaveze = moaveze;
    }
    return {

      social_priceMarks,
      social_price_items,

      minp,
      maxp,
      

      del_tavafoghi,
      conTavafoghiFn,
     
      

      moavezeMarks,
      moaveze_items,
      moavezeFn,
      group_item_name
    };
  },
};
</script>

<style></style>
