<template>
  <div class="outer" id="container">
    <h3>Tooltips with Vue 3 Teleport</h3>
    <p>{{num}}</p>
    <div class="triangle" id="triangle">

    </div>
    <a-input v-model:value="inputValue" placeholder="Basic usage"  />
    <a-button type="primary" class="btn" @click="btnClick('A')">A</a-button>
    <a-button type="primary" class="btn" @click="btnClick('B')">B</a-button>
    <a-button type="primary" class="btn" @click="btnClick('C')">C</a-button>
    <textarea  rows="2"></textarea>
    <div>
      <MyModal />
    </div>
    <div id="box1">
      <div id="box2">
        content
      </div>

    </div>
  </div>
</template>
<script>
import { onMounted,ref } from 'vue';
import MyModal from "../components/MyModal.vue"
export default {
  components: {
   MyModal
  },
  setup() {
    const num = ref(10);
    const inputValue = ref('')
    var arr = [1,2,2,3,4,5,7,8,9,10,11,22,33,44,55,66,77,105,204,425]
    // const button = ref(null);
    // const openTooltip = () =>{
    //   const target = document.querySelector('body');
    //   button.value.addEventListener('mouseover',showTooltip = true)
    //   button.value.addEventListener('mouseout',showTooltip = false)
    //   showTooltip.value = true
    // }
    // return {
    //   button,
    //   showTooltip,
    //   openTooltip
    // };
    onMounted(()=>{
      console.log("=========");
      // let timer = setInterval(()=>{
      //   if(num.value == 0){
      //     clearInterval(timer)
      //     return
      //   }
      //   num.value--
      //   console.log("倒计时===",num.value)
      // },1000)
     
      // let num1 = 10
      // var countDownFn = function(){
      //   num.value--
      //   console.log('倒计时---',num.value)
      //   if(num.value == 0){
      //     clearTimeout(timer)

      //   }else{
      //     timer = setTimeout(countDownFn,1000)
      //   }
      // }
      // var timer = setTimeout(countDownFn,1000)
      // for(let i = 1 ;i<=9;i++){
      //   for(let j =1;j<=i;j++){
      //     console.log("------九九乘法表===",j ,'*', i);
      //   }
      // }
      // 找出字符串中出现最多的字符 --start
      // let str = 'eqasdfssaaaasaasssssaa';
      // var result = new Map()
      // // var arr = []
      // for(let v of str){
      //   if(!result.has(v)){
      //     result.set(v,1)
      //     // arr.push(v)
      //   }else{
      //     let n = result.get(v)
      //     result.set(v,n+1)
      //   }
      // }
      // console.log("最后结果==",result)
      // // arr.sort((a,b)=> result.get(b) - result.get(a) )
      // // console.log("出现最多字符的是：",arr[0],'次数：',result.get(arr[0]))
      // let maxCount = Math.max(...result.values())
      // let maxChar
      // for(let [key,value] of result){
      //   if(value === maxCount){
      //     maxChar = key
      //     break
      //   }
      // }
      // console.log("出现最多字符的是：",maxChar,'次数为:',Math.max(...result.values()))

      // --end
      // start
      var $ = document.querySelector.bind(document)
      const box1 = $('#box1')
      const box2 = $('#box2')
      box1.addEventListener('click',()=>{
        console.log("box1 true");
      },true)
      box1.addEventListener('click',()=>{
        console.log("box1 false");
      },false)
      // box2.addEventListener('click',()=>{  //事件捕获
      //   console.log("box2 true");
      // },true)
      box2.addEventListener('click',()=>{ //事件冒泡
        console.log("box2 false");
      },false)
      // end
      
      // start 3 5 7 4 6 1
      // setTimeout(()=>{
      //   console.log("1");
      // },0)
      // const promise = new Promise((reslove)=>{
      //   console.log("3");
      //   reslove("4");
      // });
      // (async()=>{
      //   console.log("5");
      //   const str = await promise;
      //   console.log(str);//4
      // })()
      // promise.then(()=>{
      //   console.log('6');
      // })
      // promise.then(promise);
      // console.log("7");
      //end

      //start   //解析URL的参数
      // let url = 'https://www.baidu/#/page?id=1&name=hahah&age=148'
      // let arr = url.split('?')[1]
      // let arr1= arr.split('&')
      // let obj = {}
      // for(let i = 0 ;i < arr1.length;i++){
      //   let arr2 = arr1[i].split('=')
      //   obj[arr2[0]] = arr2[1]
      // }
      // console.log("====obj",obj);
      //end

      //start
      // console.log("==开始打印");
      // const promise1 = new Promise((reslove)=>{
      //   setTimeout(()=>{
      //     console.log("1");
      //     reslove()
      //   },1000)
        
      // });
      // const promise2 = new Promise((reslove)=>{
      //   setTimeout(()=>{
      //     console.log("2");
      //     reslove()
      //   },2000)
        
      // });
      // async function executePromise(){
      //   await promise1
      //   await promise2
      // }
      // executePromise()
      //end

      // start
     console.log("aaa");
     setTimeout(()=>{
      console.log("bbb");
     },1000)
     const start = new Date()
     while(new Date() - start < 3000){console.log("11111");}
      setTimeout(()=>{
      console.log("ccc");
     },0)
     const p1 = new Promise((reslove)=>{
      console.log("ddd");
      reslove()
      console.log(("eee"));
     })
     p1.then(()=>{
      console.log("ggg");
     })
     console.log("fff");

     // aaa ddd eee fff ggg bbb ccc
    });
    const btnClick = (type) =>{
      let value = inputValue.value
      switch(type){
        case 'A':
          
          // var parentNode = document.getElementById('container')
          var newNode = document.createElement('div')
          newNode.id = 'triangle1'
          // var referNode = parentNode.firstChild  //追加到指定的位置
          // parentNode.insertBefore(newNode,referNode)
          document.body.appendChild(newNode)
          console.log('AAAAAAAA',inputValue.value)
          if(value){
            var arr1 = arr.filter((item)=>item%10 == value)
            document.getElementsByTagName('textarea')[0].value = arr1.join(',')
          }else{
            document.getElementsByTagName('textarea')[0].value = ''
          }
          console.log("arrrrrrrrr1",arr1);
          break;
        case 'B':
          console.log('BBBBBBB')
          var delNode  = document.getElementById('triangle1')
          delNode.parentNode.removeChild(delNode) //删除节点
          if(value){
            var arr2 = arr.map(item=>{
              return item - value
            })
            document.getElementsByTagName('textarea')[0].value = arr2.join(',')
          }else{
             document.getElementsByTagName('textarea')[0].value = arr.join(',')
          }
          break;
        case 'C':
          if(value){
            arr.splice(3,0,Number(value)) //在下标为3的位置插入输入框中的值
          }
          document.getElementsByTagName('textarea')[0].value = arr.join(',')
          console.log('CCCCCC',arr)


          var oldNode = document.getElementById('triangle')
          var newNode1 = document.createElement('div')
          if(oldNode){
            oldNode.parentNode.replaceChild(newNode1,oldNode) //替换节点
          }

          break;
        default:
          console.log("其他",type,arr);
          //5 3 3 7 4 6 3 1
      }
    }
    return {
      num,
      inputValue,
      btnClick,
    }

    
  },
};
</script>
<style >
.outer{
  width: 300px;
  margin: auto;
}
.triangle{
  /* background: red; */
  width: 0px;
  height: 0px;
  border-top: 20px solid red;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  margin: auto;
}
#triangle1{
  /* background: red; */
  width: 0px;
  height: 0px;
  border-top: 20px solid red;
  border-left: 10px solid transparent;
  border-right: 10px solid transparent;
  margin: auto;
}
#box1{
  width: 100px;
  height: 50px;
  background: rgb(87, 90, 87);

}
#box2{
  width: 60px;
  margin: auto;
  background: rgb(215, 218, 215);

}
</style>
