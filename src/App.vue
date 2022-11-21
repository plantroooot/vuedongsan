<template>
  <!-- node.js - npm쓰려고 설치, @vue/cli -> vue 프로젝트 빠르게 생성해주는 라이브러리 / vue create 프로젝트명 -->
  <!-- npm run serve -> 미리보기 -->

  <!-- - vue 반복문 -->
  <!-- <tag v-for="변수이름 in 반복횟수 또는 자료형 이름" :key="작명"></tag> -->
  <!-- 
    1) key -> 반복문이 돌면서 변하는 숫자(반복한 요소들을 각각 구분짓기 때문에 반복문 돌릴때 꼭 필요함.)
    2) 작명 -> 변수명 작성
    3) 반복횟수 -> 해당 반복횟수만큼 for문이 돌아감
    4) Array, Object이름 
        - 해당 자료형에 있는 요소들의 갯수만큼 돌아감
        - 작명한 변수는 반복될때마다 메뉴들 안에있던 자료들이 됨
        - {{}}안에 넣으면 자료형이 출력됨
    5) v-for안의 변수는 2개까지 생성 가능 (작명, i) - 작명 : array안의 데이터, i - 1씩 증가하는 정수(0, 1, 2....) key안에 집어넣음
   -->
  <div class="menu">
    <a v-for="(a) in menus" :key="a">{{ a }}</a>
  </div>
  <!-- <div v-for="(room, i) in products" :key="i">
    <h4>{{ products[i] }}</h4>
    <p>50만원</p>
  </div> -->

  <!-- 불러올 컴포넌트 -->
  <!-- 컴포넌트 쓰는법 import -> 등록 -> 쓰기 -->
  <!-- 
    장점
    - 파일 깔끔하게 정리
    - HTML재사용 쉬움

    단점
    - 데이터관리가 귀찮아질수 있음.
   -->
  <Discount :discountPercentage="discountPercentage" />
  <!-- 
    *라이프사이클
    - 컴포넌트의 생성 과정을 뜻한
    
    *라이프사이클 훅(Life Cycle Hook)
    - 라이프사이클이 돌아가는 중간중간에 hook을 걸어 코드를 실행시키는 것.

   -->

  <button @click="priceSort">낮은가격순</button>
  <button @click="priceSortHigh">높은가격순</button>
  <button @click="nameSort">상품명순</button>
  <button @click="sortBack">되돌리기</button>

  <!-- 모달창 만들기 -->
  <!-- 
    0. HTML, CSS로 디자인
    1. UI의 현재 상태를 데이터로 저장해둠(해당 UI가 어떻게 보여야 하는지?) 0, 1 or true, false
    2. 데이터에 따라 UI가 어떻게 보일지 작성
   -->
   <!-- v-if="조건식" - 조건식이 참일때만 HTML보여줌 // v-else, v-else-if도 가능-->

  <!-- App.vue - 부모 컴포넌트, Modal.vue 자식 컴포넌트 -->

  <!-- <div class="start" :class="{ end : modalState }"> -->
  <Transition name="fade">
    <ModalInfo @closeModal="modalState = false" :onerooms= "onerooms" :roomNumber="roomNumber" :modalState="modalState" />
  </Transition>
  <!-- </div> -->
  
  <!-- props 문법 - 부모 컴포넌트의 데이터를 사용하고 싶을때 사용
   1. 데이터 등록 -> :작명 = "실제 데이터이름" : -> v=bind
   2. 데이터를 자식컴포넌트에 보내기
   3. 오브젝트 자료형은 v-bind="오브젝트이름" -> 한번에 전송가능
    ex) <Discount :name="obj.name" :age="obj.age" v-bind="obj" />
   4. HTML을 여러개 만들어(for문 등) 컴포넌트에 저장하기 보다는 하나의 HTML을 컴포넌트에 저장하여 가져다쓰는게 재사용이 쉬움.
   -->
   <!-- :class="{ 클래스명 : 조건 }" - class명을 조건부로 넣을 수 있음. -->
   <!-- <Transition name="작명"></Transition> -> vue에서 제공함. -->

  

  <!-- 이벤트핸들러 - v-on::(@) -->
  <!-- ++ -> 1증가 항상 데이터를 기획해야함-->
  <!-- <div v-for="(room, i) in products" :key="i">
    <h4>{{products[i]}}</h4>
    <p>50만원</p>
    <button @click="reportNum[i]++">허위매물신고</button> <span>신고수 : {{ reportNum[i] }}</span>
  </div> -->


  <!--src에 있는거 가져올때는 ./부터 시작함 -->
  <!-- <div> 새로운 데이터로 만듬
    <img src="./assets/room0.jpg" class="room-img">
    <h4 @click="modalState = true">{{products[0]}}</h4>
    <p>60만원</p>
    <button @click="reportNum[0]++">허위매물신고</button>
    <span>신고수 : {{ reportNum[0] }}</span>
  </div>  
  <div>
    <img src="./assets/room1.jpg" class="room-img">
    <h4>{{products[1]}}</h4>
    <p>40만원</p>
    <button @click="reportNum[1]++">허위매물신고</button>
    <span>신고수 : {{ reportNum[1] }}</span>
  </div>
  <div>
    <img src="./assets/room2.jpg" class="room-img">
    <h4>{{products[2]}}</h4>
    <p>70만원</p>
    <button @click="reportNum[2]++">허위매물신고</button>
    <span>신고수 : {{ reportNum[2] }}</span>
  </div> -->

   <!-- <div v-for="(rooms, i) in onerooms" :key="i">
        <img :src="onerooms[i].image" class="room-img">
        <h4 @click="modalState = true; roomNumber = i">{{onerooms[i].title}}</h4>
         <h4>{{onerooms[i].title}}</h4>
        <p>{{onerooms[i].price}}원</p>
    </div> -->

  

  <Card @openModal="modalState = true; roomNumber = $event" :oneroom="onerooms[i]" v-for="(rooms, i) in onerooms" :key="i" />
  <!-- @작명="자바스크립트 코드"  -> 자식컴포넌트에서 보낸 $emit의 메세지를 수신함. -->
  <!-- 자식컴포넌트에서 보낸 $emit의 데이터는 $event에 저장되어 있음. -->
  <!-- <Card :oneroom="onerooms[1]" />
  <Card :oneroom="onerooms[2]" />
  <Card :oneroom="onerooms[3]" />
  <Card :oneroom="onerooms[4]" />
  <Card :oneroom="onerooms[5]" /> -->

  

  


  
</template><!-- html짜기 -->


<script> //script짜기

import data from './assets/oneroom.js' //import 변수명 from './assets/oneroom.js
import Discount from './Discount.vue';
import ModalInfo from './ModalInfo.vue';
import Card from './Card.vue';



//중괄호 사용시 import {}로 작성

//1. 데이터바인딩
//데이터바인딩 하는 이유 
//- 하드코딩시 변경 어려움
//- 실시간 자동 렌더링 쓰기위해 - (data변경시 관련 HTML파일 전부에 실시간으로 반영됨 - 부드럽게 전환됨)
//- 자주 변경될 데이터들은 밑에 저장해놨다가 데이터 바인딩으로 꽂아줌. {{data() - return안에 있는 key값}}
//*** html의 속성에도 데이터바인딩 가능 - :속성="데이터이름"

export default {
  name: 'App',
  data(){
    return {
      //데이터 보관함 - object자료형, array로 기입
      oneroomsorg : [...data], //[...array자료] - array / object데이터의 각각 별개의 사본을 만들기
      products : ['역삼동 원룸', '천호동원룸', '마포구원룸'],
      menus : ['Home', 'Shop', 'About'],
      reportNum : [0, 0, 0],
      modalState : false, //UI의 상태 저장
      onerooms : data,
      roomNumber : 0,
      obj : { name : 'min', age : '31'},
      showDiscount : true,
      discountPercentage : 30,
    }
  },
  methods :{ //vue에서 함수는 전부 여기서 만듬! - html에는 함수명만 사용!
    increase(){ //data의 자료를 가져다 쓸때는 this.이름으로 시작해야함!
      this.reportNum += 1;
    },
    sortBack(){
      this.onerooms = [...this.oneroomsorg];
      //**** 등호로 array를 집어넣으면 왼쪽과 오른쪽의 값을 공유해주세요~라는 뜻이 됨.
      //개별 복사본을 만들어 넣어야됨.
    },
    priceSort(){
      // sort(); -> array속 숫자들을 오름차순으로 정렬함.
      /* array.sort(function(a, b){ //정확한 숫자의 오름차순 정렬
        return a - b // 이부분이 음수면 a를 왼쪽으로, 양수면 a를 오른쪽으로 이동시킴, 원본이 변형됨
      }) */
      this.onerooms.sort(function(a, b){
        return a.price - b.price; //object안의 가격을 불러옴
      });
    },
    priceSortHigh(){
      this.onerooms.sort(function(a, b){
        return b.price - a.price;
      })
    },
    
    nameSort(){
      this.onerooms.sort(function(a, b){
        if(a.title.toUpperCase() < b.title.toUpperCase()){
          return -1
        }
        if(a.title.toUpperCase() > b.title.toUpperCase()){
          return 1
        }
        return 0;
      });
    }
    //50만원 이하 상품 필터기능 만들기
  },

  // created(){ //HTML 생성 후 실행 - ajax요청시 사용

  // },

  mounted(){ //마운트 이후 코드 실행
    // setTimeout(()=>{ //arrow function을 사용해야함(바깥의 this를 잘 가져다 쓸 수 있음.)
    //   this.showDiscount = false;
    // }, 2000);
    
    setInterval(() => {
      if(this.discountPercentage == 0){
        clearInterval();
      }else{
        this.discountPercentage-=1;
      }
    }, 1000);    
  },

  components: {//컴포넌트 등록
    Discount : Discount, //왼쪽은 자유작명 - 오른쪽은 import명 왼쪽 이름 == 오른쪽이름일경우 1개만 써도 됨.
    ModalInfo : ModalInfo,
    Card : Card,
  }
}


</script>

<style>/* css */
body{
  margin:0;
}
div{
  box-sizing:border-box;
}
.discount{
  background-color:#eee;
  padding:10px;
  margin:10px;
  border-radius: 5px;
}
.black-bg{
  width:100%; height:100%;
  background:rgba(0, 0, 0, 0.5);
  position:fixed; left:0; top:0; padding:20px;
}
.white-bg{
  width:100%; background:white;
  border-radius:8px;
  padding:65px 20px 20px;
  position: relative;
}
.white-bg .close-btn{
  width:60px; height:30px; line-height:30px;
  font-size:13px; font-weight:400; color:#fff;
  position: absolute; right:20px; top:20px;
  background-color:#000; border:0;
  cursor:pointer;
}
.white-bg img{
  width:100%;
}
.room-img{
  width:100%;
  margin-top:40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.menu{
  background:darkslateblue;
  padding:15px;
  border-radius:5px;
}
.menu a{
  color:#fff;
  padding:10px;
  text-decoration:none;
}

.start{
  opacity:0;
  transition: all 1s;
}

.end{
  opacity:1;
}

/* vue 애니메이션 */
/* 
   - 시작시
  작명-enter-from - 시작시 스타일
  작명-enter-active - transition
  작명-enter-to - 끝날시 스타일

  - 퇴장시
  작명-leave-from - 시작시 스타일
  작명-leave-active - transition
  작명-leave-to - 끝날시 스타일

*/
.fade-enter-from{
  opacity:0;
  /* transform:translateY(-1000px); */
}
.fade-enter-active{
  transition:all 0.4s;
}
.fade-enter-to{
  opacity:1;
  /* transform:translateY(0); */
}

.fade-leave-from{
  opacity:1;
}
.fade-leave-active{
  transition:all 0.4s;
}
.fade-leave-to{
  opacity:0;
}


</style>
