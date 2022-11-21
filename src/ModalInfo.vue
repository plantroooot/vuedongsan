<template>
    <div class="black-bg" v-if="modalState == true">
        <div class="white-bg">
            <button class="close-btn" @click="$emit('closeModal')">닫기</button>
            <img :src= "onerooms[roomNumber].image" style="width:100%;"> 
            <h4>{{ onerooms[roomNumber].title }}</h4>
            <p>{{ onerooms[roomNumber].content }}</p>
            <!-- <input type="text" @input="month = $event.target.value" /> -->
             <!-- 
                1. @input -> input태그에 입력할때마다 이벤트 실행, @change -> input에 입력하고 다른데 클릭하면 이벤트실행
                2. $event -> 자바스크립트의 function(e)와 똑같은 의미.
                3. 사용자가 input에 입력한 것은 전부 문자 자료형이됨.
             --> 
            <input type="text" v-model="month" />
            <!-- <select v-model="month">
                <option>안녕하세요.</option>
                <option>반갑습니다.</option>
            </select> -->
            <!-- <input type="checkbox" v-model="month"> -->
            <!-- 
                1. input류의 모든 태그에 사용 가능(input, button, textarea, select...)
                2. 입력시 데이터를 state에 바로 저장하는 문법
                3. v-model.number - 입력한 것을 전부 숫자자료형으로 변경시켜줌.
                4. checkbox / radio의 경우 값을 true, false로 반환.
            -->
            <p style="margin-top:10px;">{{ month }}개월 선택함 : {{ onerooms[roomNumber].price * month }}원</p>
        </div> 
    </div>
</template>

<script>
export default {
    name : 'ModalInfo',
    data(){
        return {
            month : 1,
        }
    },
    // watch : {//watcher - 데이터 감시기능
    //     month(val, e){ //data명과 똑같은 함수명 사용
    //         //사용자가 month를 글자로 입력하면 경고문을 띄우기 / 파라미터 - data자료임
    //         // if(val >= 13){ //변경전 데이터, 변경 후 데이터
    //         //     alert('0~13까지 입력 가능합니다.');
    //         //     this.month = '';
    //         // }
    //         var regexp = /^[0-9]*$/;

    //         if(!regexp.test(val)){                
    //             this.month = 1;
    //             if(e.isComposing){
    //                 return
    //             }
    //             alert('숫자만 입력가능합니다.');

    //         }else{
    //             parseInt(val);
    //         }


    //     }
    // },
    // beforeUpdate(){
    //     if(this.month == 2){
    //         this.month = 3;
    //         alert('3개월 이상부터 가능합니다.');
    //     }
    // },
    props : {
        onerooms : Array, //데이터의 자료형을 기입(Array, Object, String...)
        roomNumber : Number,
        modalState : Boolean, // = 로 재할당 안됨 - read-only
    }
}
</script>

<style>

</style>