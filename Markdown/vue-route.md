# Vue-routerで遷移時にパラメタを渡す

vue-routerで画面遷移時にパラメータ渡すのに手詰まったのでメモ

## サンプルのvue-routerのルーティング
pathにはパターンを書きます。```:```を先頭に書くのはrailsのroutesと同様ですね。  
```js
import Vue from 'vue'
import Router from 'vue-router'

Vue.use(Router)

export default new Router({
  routes: [
    {
      path: '/',
      name: 'index-page',
      component: require('@/components/index').default
    },
    {
      path: '*',
      redirect: '/'
    },
    {
      path: 'fuga',
      name: 'fuga-view',
      component: require('@/components/fuga').default
    },
    {
      path: '/hoge/:value',
      name: 'hoge-view',
      component: require('@/components/hoge').default
    }
  ]
})

```
## リンク元ページ  

リンク元でrouter-linkタグを使ってリンクを張ります。toの中身はハッシュで渡していきます。

```js
<template>
  <div id="wrapper">
        <router-link :to="{ name: 'hoge-view', params: { value: 'test value' }}" >hoge Link</router-link >
        <router-link :to="{ name: 'fuga-view' }" >fuga Link</router-link >
    </main>
  </div>
</template>
  
```

## リンク先ページ
リンク先は通常変数と同様に展開します。

```js
<template>
  <div>
    <router-link :to="{ name: 'index-page' }"> back </router-link>
    This is hoge page.   value is {{ $route.params.value }} 
  </div>
</template>
```

## リンクが変更されたときに関数を呼び出す

変更に合わせて関数を呼び出す場合はvueに用意されているウォッチャーを使います


```js
new Vue({
  components: { App },
  router,
  store,
  template: '<App/>',
  watch: {
    $route: function (to, from) {
      // ここにコードを書く
    }
  }
}).$mount('#app')

```

