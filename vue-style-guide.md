# Vue Style Guide (Official)

## Index

- 1. Introduction
- 2. 우선순위 A: 필수
- 3. 우선순위 B: 매우 추천함
- 4. 우선순위 C: 추천함
- 5. 우선순위 D: 주의요함

## 01. Introduction

이 문서는 `Vue` 코드에 대한 공식 스타일 가이드입니다.

## 02. 우선순위 A: 필수

### 컴포넌트 이름에 합성어 사용

항상 두글자이상으로 컴포넌트 이름을 생성합니다.

Bad:

```javascript
Vue.component('todo', {...});
```

Good:

```javascript
Vue.component('todo-item', {...});
```

### 컴포넌트의 `data`는 반드시 함수여야 합니다.

Bad:

```javascript
Vue.component("some-comp", {
  data: {
    foo: "bar",
  },
});

export default {
  data: {
    foo: "bar",
  },
};
```

Good:

```javascript
Vue.component("some-comp", {
  data: function{
    foo: "bar",
  },
});

export default {
  data() {
    return {
      foo: "bar"
    }
  }
}
```

### Prop은 가능한 상세하게 정의되어야 합니다.

Bad:

```javascript
props: ["status"];
```

Good:

```javascript
props: {
  status: {
    type: String,
    required: true,
    validator: function(value) {
      return [
        'syncing',
        'synced',
        'version-conflict',
        'error'
      ].indexOf(value) !== -1
    }
  }
}
```

### `v-for`는 `key`와 항상 함께 사용합니다.

Bad:

```html
<ul>
  <li v-for="todo in todos">
    {{ todo.text }}
  </li>
</ul>
```

Good:

```html
<ul>
  <li v-for="todo in todos" :key="todo.id">
    {{ todo.text }}
  </li>
</ul>
```

### `v-for`가 사용된 앨리먼트에 절대 `v-if`를 사용하지 마세요.

Bad:

```html
<ul>
  <li v-for="user in users" v-if="user.isActive" :key="user.id">
    {{ user.name }}
  </li>
</ul>
```

Good:

```html
<ul>
  <li v-for="user in activeUsers" :key="user.id">
    {{ user.name }}
  </li>
</ul>
```

### 컴포넌트 스타일은 스코프로 설정한다.

Bad:

```html
<template>
  <button class="btn btn-close">X</button>
</template>

<style>
  .btn-close {
    background-color: red;
  }
</style>
```

Good:

```html
<template>
  <button class="btn btn-close">X</button>
</template>

<style scoped>
  .btn-close {
    background-color: red;
  }
</style>
```

### Private 프로퍼티에는 항상 접두사 `$_`를 사용하고 named scope를 포함하라.

Bad:

```javascript
var myGreatMixin = {
  methods: {
    $_update: function () {
      // ...
    },
  },
};
```

Good:

```javascript
var myGreatMixin = {
  methods: {
    $_myGreatMixin_update: function () {
      // ...
    },
  },
};
```

## 03. 우선순위 B: 매우 추천함

## 04. 우선순위 C: 추천함

## 05. 우선순위 D: 주의요함
