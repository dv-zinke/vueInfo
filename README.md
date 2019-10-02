Vue.js
(Vue 2.x 문서 참고)
======


[vue-router](./vue-router)
[vuex](./vuex)


뷰는 MVVM 패턴과 관련이 없지만 부분적으로 그것에 영감을 받음


MVC - 아키텍처의 최상위에 뷰가 있고 그아래 컨트롤러가 있고 그 아래 모델이 있습니다. 때문에 뷰는 컨트롤러만 알고 있고 컨트롤러는 모델을 알고 있습니다. 모델이 변경되었을 때 뷰는 컨트롤러를 통해서 통보를 받습니다.

MVP - MVC에서 컨트롤러가 Presenter로 교체된 형태이고 프리젠터는 뷰와 같은 레벨에 있습니다. 프리젠터는 뷰와 모델의 이벤트를 모두 받으면서 둘 사이의 상호작용을 조정합니다.

MVVM - MVC에서 컨트롤러가 뷰모델로 교체된 형테이고 뷰모델은 UI레이어 아래에 위치합니다. 뷰모델은 뷰가 필요로 하든 데이터와 커맨드 객체를 노출해 주기 때문에 뷰가 필요로하는 데이터와 액션은 담고 있는 컨테이너 객체로 볼 수도 있습니다.


뷰 라이프사이클
-----------

### beforeCreate 
가장 먼저 실행되는 훅 아직 data와 event가 세팅되지않은 시점

### created 
data와 events가 호ㅘㄹ성화 된 시점 여전히 템플릿,가상돔은 마운트 및 렌더링 되지않은 시점

### beforeMount 
템플릿,렌더함수들이 컴파일된후 첫 렌더링이 일어나기직전 실행 됨, 왠만한 경우 사용하지 않는 것이 좋다. 그리고 서버사이드렌더링시에는 호출되지않는다.

### mounted
컴포넌트, 템플릿, 렌더링 된 돔에 접근 할수 있다. 모든 하위 컴포넌트가 마운트된 상태를 보장 하지 않는다. beforeMount와 마찬가지로 서버렌더링에서는 호출되지않는다.
유의할점)  부모와 자식관계의 컴포넌트에서 우리가 생각한 순서로 mounted가 발생하지 않는다

### beforeUpdate 
컴포넌트 데이터가 변하여 업데이트 사이클이 시작될때 실행 됨 여기서 변경할때 렌더링은 트리거되지않음

### updated
데이터가 변하여 재 렌더링이 일어난후에 실행된다 여기서 상태변경하면 무한루프에 빠질수있음. 모든 자식 컴포넌트의 재 렌더링 상태를 보장하지않음

### beforeDestory 
뷰 인스턴스가 제거되기 직전에 호출딘다 이벤트 리스너를 제거하거나 reactive subscription을 제거 하고자 한다면 이 훅이 제격, 서버렌더링시 호출되지않는다.

### destoryed
Vue 인스턴스의 모든 디렉티브가 바인딩 해제되고 모든 이벤트리스너가 제거되며 모든 하위 Vue 인스턴스도 삭제된다. 서버렌더링시 호출되지않음

### etc
activated와 deactivated가 있다. 각각 keep-alive 컴포넌트가 활성화 될 때와 비활성화 될 때 호출된다.
# 라이프사이클 다이어그램
![Alt text](https://kr.vuejs.org/images/lifecycle.png)