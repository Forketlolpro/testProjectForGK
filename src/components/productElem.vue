<template>
  <li class="product">
    <div class="image-spot">
      <a class="image-a">
        <img :src=imageURL>
      </a>
    </div>
    <div class="specification-spot">
      <p class="code">Код: {{code}}</p>
      <a class="title">{{item.title}}</a>
      <div class="product-tag">
        <p>Могут понадобиться: </p><tag-list v-bind:tags="item.assocProducts.split(';\n')"></tag-list>
      </div>
    </div>
    <div class="cost-spot">
      <p class="product-availability">Наличие</p>
      <div class="cost">
      <span class="club-c">По карте<br>&nbsp&nbsp&nbsp&nbsp&nbspклуба</span>
        <div class="cost-number"><p class="price-gold">{{cardPrice}}&nbsp&#8381</p><br><p class="price-retail">{{price}}&nbsp&#8381</p></div>
      </div>
      <div class="bye-spot">
        <span class="bonuses">Можно купить за 231,75 балла</span><br>
        <span v-on:click="clickOnMeter" :class="[meterIsActive ?'active': 'no-active']"class="bye-meter">За м. кв.</span><span v-on:click="clickOnPack" :class="[packIsActive ?'active': 'no-active']" class="bye-pack">За упаковку</span>
        <span class="popup">Продается упаковками:<br>1 упаковка = 2.47 м. кв.</span>
        <button v-bind:data-product-id='this.item.productId' class="btn">В КОРЗИНУ</button>
        <div class="stepper">
          <input class="stepper-input" type="text" v-model="stepValue"/>
          <span class="up" v-on:click=stepValueChange(1)></span>
          <span class="down" v-on:click=stepValueChange(-1)></span>
        </div>
      </div>
    </div>
  </li>
</template>

<script>
    import TagList from "./tagList";
    export default {
      components: {TagList},
      methods:{
        stepValueChange:function(count){
          this.stepValue=this.stepValue+count;
          if (this.stepValue<0) this.stepValue=0;
        },
        clickOnMeter:function () {
          this.meterIsActive=true;
          this.packIsActive=false;
        },
        clickOnPack: function () {
          this.packIsActive=true;
          this.meterIsActive=false;
        }
      },

      mounted: function(){
        this.item.assocProducts.split('\n').forEach((item)=>{

        })
      },
      props:['item'],
      data () {
        return {
          stepValue:1,
          meterIsActive:true,
          packIsActive:false,
        }
      },
      computed:{
        price:function(){
          return (this.meterIsActive==true)?this.item.priceRetailAlt.toFixed(2):this.item.priceRetail.toFixed(2);
        },
        cardPrice:function(){
          return (this.meterIsActive==true)?this.item.priceGoldAlt.toFixed(2):this.item.priceGold.toFixed(2);
        },
        code: function () {
          return parseInt(this.item.code);
        },
        imageURL:function () {
          let tmp = this.item.primaryImageUrl.split('');
          tmp.splice(-4,0,'_','2','2','0','x','2','2','0','_','1');
          return tmp.join('');
        }
      },
    }
</script>

<style lang="scss" scoped>
.product{
  font-family: Arial, Helvetica, sans-serif;
  position: relative;
  width: 1000px;
  height: 305px;
  border: 1px solid #bcbcbc;
  margin: 5px;
}
.image-spot{
  box-sizing: border-box;
  position: absolute;
  height: 100%;
  width: 200px;
}
  img{
    max-height: 160px;
    max-height: 160px;
  }
  .image-a{
    cursor: pointer;
    box-sizing: border-box;
    display: block;
    margin: 10px 20px 20px 20px;
    width: 160px;
  }
  .specification-spot{
    box-sizing: border-box;
    position: absolute;
    left: 200px;
    height: 100%;
    width: 510px;
  }
  .code{
    color: grey;
    font-size: 12px;
  }
  .title{
    word-wrap: break-word;
    font-size: 16px;
    font-weight: 700;
    line-height: 24px;
  }
  .title:hover{
    cursor: pointer;
    text-decoration: underline;
  }
  .product-tag{
    margin-top: 20px;
  }
  .product-tag *{
    display: inline;
  }
  .product-tag p{
    font-size: 13px;
    line-height: 16px;
    color: #545454;
    font-weight: 700;
  }
.cost-spot{
  box-sizing: border-box;
  width: 290px;
  height: 100%;
  position: absolute;
  right: 0;
}
  .product-availability{
    position: absolute;
    margin: 0px;
    top: 5px;
    right: 5px;
    color: #093;
    border-bottom: 1px dotted #093;
  }
  .product-availability:hover{
    cursor: pointer;
    border: none;
  }
  .cost{
    box-sizing: border-box;
    position: absolute;
    top: 39px;
    height: 100px;
    width: 100%;
  }
  .club-c{
    position: absolute;
    left: 110px;
    font-size: 14px;
    line-height: 17px;
  }
  .cost-number{
    position: absolute;
    top: 15px;
    left: 167px;
    width: 120px;
    text-align: right;
  }
  .cost-number p {
    margin: 0px;
    display: inline;
  }
  .price-gold{
    font-size: 25px;
    font-weight: 700;
    color: #000;
  }
  .price-retail{
    color: #a7a7a7;
    font-size: 25px;
  }
  .bye-spot{
    position: absolute;
    width: 100%;
    top: 120px;
    height: 160px;
    text-align: right;
  }
  .bye-spot :first-child {
    font-size: 12px;
    line-height: 17px;
    color: #999;
  }
  .bye-spot :nth-child(n){
    margin-right: 5px;
  }
  .bye-meter{
    padding: 3px 0;
    font-size: 13px;
    line-height: 13px;
  }
  .bye-pack{
    padding: 3px 0;
    font-size: 13px;
    line-height: 13px;
  }
  .active{
    background: #000;
    cursor: default;
    color: #fff;
    border-bottom: 1px solid transparent;
  }
  .no-active{
    color: #707070;
    border-bottom: 1px dotted #707070;
    cursor: pointer;
  }
  .btn{
    position:absolute;
    height: 41px;
    width: 150px;
    left: 136px;
    top:90px;
    background-color: #f90;
    color: white;
    border: none;
    font: 14px/40px Arial,Helvetica,sans-serif;
  }
  .stepper{
    position: absolute;
    top: 90px;
    left: 70px;
  }
  .stepper-input{
    width: 40px;
    padding: 12px 0 10px;
    font-size: 13px;
    line-height: 1.2;
    overflow: hidden;
    text-align: center;
    border-width: 1px 0px 1px 1px;
    border-color: #ccc;
    border-style: solid;
  }
  .up{
    cursor: pointer;
    display: block;
    position: absolute;
    top: 0px;
    left: 41px;
    background: url("../icons/up-arrow.png") no-repeat #fff;
    width: 20px;
    height: 20px;
    border: 1px solid #ccc;
  }
  .down{
    display: block;
    position: absolute;
    top:20px;
    left: 41px;
    background: url("../icons/down-arrow.png") no-repeat #fff;
    width: 20px;
    height: 19px;
    border: 1px solid #ccc;
  }
  .down:hover{
    cursor: pointer;
    background: url("../icons/down-arrow-whith.png") no-repeat #060606
  }
.up:hover{
  cursor: pointer;
  background: url("../icons/up-arrow-whith.png") no-repeat #060606
}
  .popup{
    position: absolute;
    display: block;
    width: 209px;
    text-align: center;
    left: 75px;
    top: 48px;
    border: 1px solid #ccc;
    font-size: 13px;
    line-height: 15px;
  }
.popup::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 10%;
  margin-left: -5px;
  border: 5px solid transparent;
  border-top-color: #ccc;
}
</style>
