<template>
  <!-- 컴포넌트 : 너무 긴 태그들을 하나의 태그로 축약가능-->
  <!-- vue파일 생성(.vue) -> 축약할 HTML 넣기 -> app.vue에 저장. -> name속성 넣기-->
  <div class="discount">
    <h4>지금 결제하면 {{ discountPercentage }}% 할인</h4>
  </div>
</template>

<script>
export default {
    name: 'Discount',
    props : {
      discountPercentage : Number,
    }
}
</script>

<style>

</style>