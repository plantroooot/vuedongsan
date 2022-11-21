<template>
    <div>
        <img :src="oneroom.image" class="room-img">
        <!-- <h4 @click="modalState = true; roomNumber = i">{{onerooms[i].title}}</h4> 오브젝트에서 꺼내옴 -->
        <h4 @click="fModal">{{oneroom.title}}</h4>
        <!-- custon event문법 - $emit('작명', 데이터) 부모요소에 메시지를 보냄(데이터 수정해주세요~) -->
        <!--  -->
        <p>{{oneroom.price}}원</p>
    </div>
</template>

<script>
export default {
    name : 'Card',
    props : {//props - 데이터 수정 금지 - read-only
        oneroom : Object,
        roomNumber : Number,
    },
    methods : {
        fModal(){
            this.$emit('openModal', this.oneroom.id); //html안의 데이터를 함수에서 사용할시 꼭 this를 붙여야함($emit, object, array등등)
        }
    }
}
</script>

<style>

</style>