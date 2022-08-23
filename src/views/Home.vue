<template>
  <div>{{state.foo}}</div>
  <p>{{state.bar}}</p>
  <p>{{sex}}</p>
  <p>{{age}}</p>
  <p>{{sum}}</p>
  <p>这里是调用computed{{sumComputed}}</p>
  <p>这里是调用computed{{sumComputed}}</p>
  <p>这里是调用computed{{sumComputed}}</p>
  <p>这里是调用Function{{sumFunction()}}</p>
  <p>这里是调用Function{{sumFunction()}}</p>
  <p>这里是调用Function{{sumFunction()}}</p>
  <p>numWatch:{{numWatch}}</p>
  <p>dataWatch:{{dataWatch.foo.car.c1}}</p>
</template>

<script>
import { isRef,ref,unref,toRef, reactive,toRefs, isProxy,computed,watch, watchEffect} from "vue"
export default {
  setup(){
    const name = ref('哈哈')
     // 1. isRef 检查某个值是否为 ref。
    if(isRef(name)){
      console.log("是");
    }else{
      console.log("不是");
    }
    // 2.判断 如果是ref对象，直接获取返回值
    const getRefValue = unref(name)
    console.log(getRefValue);
    // 3.toRef 转换的对象是引用类型，源数据会被影响
    const state = reactive({
      foo:1,
      bar:2
    })
    const fooRef = toRef(state,'foo')
    fooRef.value++ 
    console.log(state.foo); //2
    state.foo++;
    console.log(fooRef.value);//3


    // 4.toRefs 将一个响应式对象转换为一个普通对象，获取变量时就不需要再加上具体的对象名
    const obj = reactive({
      sex:'男',
      age:'18'
    })
    // 5. isProxy() 检查一个对象是否是由 reactive()、readonly()、shallowReactive() 或 shallowReadonly() 创建的代理。
    if(isProxy(obj)){
      // console.log("isProxy");
    }else{
      // console.log("非isProxy");
    }
    // 6. computed 响应式依赖
    const number = ref(1);
    const age = ref(10);
    const sum = computed(() => number.value + age.value) //只要有一个值发生变化，sum就会改变
    /*setTimeout(()=>{
      number.value = 20
    },1000)
    setTimeout(()=>{
      age.value = 30
    },2000)*/
    /*const sum = computed({
      get:()=> number.value + age.value,
      set: (value)=>{
        number.value = value + 5 
      }
    })
    setTimeout(()=>{
      sum.value = 20 //这里先执行sum 中的set 方法，之后number 就变成 40 ，因为number 值发生了改变，所以会触发sum 的get方法，最终sum输出的结果为 20 + 5 + 10
    },2000)*/
    //缓存机制
    const sumComputed = computed(()=>{
      // console.log("这里是调用computed"); //上面调用了三次，只会打印一次
      return number.value + 10
    })
    const sumFunction = ()=>{
      // console.log("这里是调用Function"); //调用多少次就会执行多少次
      return number.value + 10
    }

    // 7. watch 侦听一个或多个响应式数据源，并在数据源变化时调用所给的回调函数。
    const numWatch = ref(1)
    const dataWatch = reactive({
      age:18,
      foo:{
        car:{
          c1:'本田'
        }
      },
      gender:'男',
      number:10
    })
    // 7.1 单个监听ref定义的变量
    // watch(numWatch,(newValue,preValue)=>{ //只要numWatch 发生改变就会触发
    //   console.log("新的值:",newValue);
    //   console.log("旧的值:",preValue);
    // })
    // 7.2 监听reactive 定义的对象
    // watch(()=>dataWatch,(newValue,preValue)=>{ //监听ref 定义的变量 只要numWatch 发生改变就会触发
    //   console.log("新的值:",newValue);
    //   console.log("旧的值:",preValue);
    // },{ //这里可以新增属性字段
    //   deep:true  //深度监听
    // })

    //7.3监听多个字段
    // watch(
    //   [()=>dataWatch.age,()=>dataWatch.gender,()=>dataWatch.number],
    //   // 第一个数组是新数据，第二个是原始数据
    //   ([newAge,newGender,newNumber],[preAge,preGender,preNumber])=>{
    //     console.log("这里是新数据:",newAge,newGender,newNumber);
    //     console.log("这里是原始数据:",preAge,preGender,preNumber);
    //   })

    // 7.4立即执行 \ 深度监听 deep
    watch(
      // ()=>dataWatch,
      // (newNumber,preNumber)=>{
      //   console.log("这里是新数据:",newNumber);
      //   console.log("这里是原始数据:",preNumber);
      // },
      // {
      //   // immediate:true, //立即执行
      //   deep:true
      // }
    )

    //7.5 watchEffect 
    const textAsync = (value)=>{
      return setTimeout(()=>{
        console.log("value================",value)
      },3000)
    }
    watchEffect(async(onCleanup)=>{
      const timer = textAsync(numWatch.value)
      // 只有依赖响应的变量发生变化时，才会执行
      onCleanup(()=>{
        console.log("22222222222")
        clearTimeout(timer)
      })
    })

    
    setTimeout(()=>{
      numWatch.value++
      // dataWatch.age = 1
      dataWatch.foo.car.c1 = '是是是'
      dataWatch.gender = '女'
    },1000)
    return {state,...toRefs(obj),sum,sumComputed,sumFunction,numWatch,dataWatch}
  }
}
</script>

<style>

</style>