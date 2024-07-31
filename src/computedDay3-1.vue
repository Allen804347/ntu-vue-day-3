<script setup>
import { ref, computed, watch } from 'vue'

    const price = ref(2);
    price.value = 100 // 設定 ref 對象時，必須透過 .value
    console.log(price.value) // 提取 ref 對象的數值時，也必須透過 .value

    const discount = ref(0.1);
    const discountedPrice = ref(0);

    function get_final_price() { // 有名字函數
      const final_price = price.value * (1 - discount.value)
      return final_price
    }

    const my_function_2 = function() { // 用變數承接 匿名函數
      const final_price = price.value * (1 - discount.value)
      return final_price
    }

    const my_function_3 = () => { // 箭頭函數
      const final_price = price.value * (1 - discount.value)
      return final_price
    }

    const my_function_4 = () => price.value * (1 - discount.value) // 簡化箭頭函數
    // 上面是四種常見的 function 寫法，在這個範例裡，他們的效果一樣

    const my_final_price = get_final_price() // 呼叫函數取得計算過後的價格
    console.log(my_final_price)

    const discountedPriceFromComputed = computed(get_final_price); // computed 要傳入的事函數，也就是計算的方法

    watch(
      [price, discount], // price | [price, discount, property] | () => {}，第一個參數是監視的對象，一般來說有這三種寫法
      (
        // [newPrice, newDiscount], [oldPrice, oldDiscount] // 可以透過解構快速拿出對應位置的參數
        newValues, oldValues
      ) => {
        const newPrice = newValues[0]
        const newDiscount = newValues[1]
        const oldPrice = oldValues[0]
        const oldDiscount = oldValues[1]

        discountedPrice.value = newPrice * (1 - newDiscount);
        console.log(`watch 計算折扣價，新的價格是 ${discountedPrice.value}`);
      },
      {
        immediate: true // 立即執行
      }
    );

    const incrementPrice = () => {
      price.value += 10;
    };

</script>

<template>
  <p>原價：{{ price }}</p>
  <p>折扣：{{ discount }}</p>
  <p>折扣價 watch：{{ discountedPrice }}</p>
  <p>折扣價 computed：{{ discountedPriceFromComputed }}</p>
  <button @click="incrementPrice">增加價格</button>
</template>
