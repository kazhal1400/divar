<template>
  <div class="" v-if="group_item_name == 'موبایل و تبلت'">
    <mobileva-tablet />
  </div>
  <div class="" v-if="group_item_name == 'رایانه'">
    <raiane />
  </div>
  <div class="" v-if="group_item_name == 'کنسول، بازی ویدئویی و آنلاین'">
    <CosoleBazi />
  </div>
  <div class="" v-if="group_item_name == 'صوتی و تصویری'">
    <soti />
  </div>
  <div class="" v-if="group_item_name == 'تلفن رومیزی'">
    <tell />
  </div>
  <cllapse-btnone
    :data_items="status_items"
    :marks="statusMarks"
    @dataFn="statusFn"
    id="status"
    exm="انتخاب"
  />

  <hr />
<cllapse-btntwo
    :price_items="electriciti_price_items"
    :marks="electriciti_priceMarks"
    @minp="minp"
    @maxp="maxp"
    id="electriciti_price"
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
import MobilevaTablet from "./electrisite/MobilevaTablet.vue";
import Raiane from "./electrisite/Raiane.vue";
import CosoleBazi from "./electrisite/CosoleBazi.vue";
import Soti from "./electrisite/Soti.vue";
import Tell from "./electrisite/Tell.vue";
import CllapseBtntwo from "../UI/CllapseBtntwo.vue";
import CllapseBtnone from "../UI/CllapseBtnone.vue";
import MovingBtn from "../UI/MovingBtn.vue";
export default {
  components: {
    MobilevaTablet,
    Raiane,
    CosoleBazi,
    Soti,
    Tell,
     CllapseBtntwo,
    CllapseBtnone,
    MovingBtn,
  },
  setup() {
     const info = inject("info");
    const group_item_name = computed(() => info.group_item_name);
    const electriciti_priceMarks = computed(() => info.subItem.electriciti_price);
    const electriciti_price_items = ref(["قیمت", "حداقل", "حداکثر"]);
    const statusMarks = computed(() => info.subItem.status);
    const status_items = ref("وضعیت کالا");

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

    function statusFn(status) {
      info.status = status;
    }
    function moavezeFn(moaveze) {
      info.moaveze = moaveze;
    }
    return {

      electriciti_priceMarks,
      electriciti_price_items,

      minp,
      maxp,
      

      del_tavafoghi,
      conTavafoghiFn,
     
      statusMarks,
      status_items,
      statusFn,

      moavezeMarks,
      moaveze_items,
      moavezeFn,
      group_item_name
    };
  },
};
</script>

<style></style>
