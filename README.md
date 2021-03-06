# TIL
Today I learned `¯\_(ツ)_/¯`


## Unix Command

* *nohup* - no hang up. 프로세스 백그라운드 실행
    * http://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_nohup_%EC%82%AC%EC%9A%A9%EB%B2%95
    * http://changpd.blogspot.kr/2013/04/linux-nohup-xxxsh.html
* *crontab* - 작업 스케줄러
    * 주기 설정정보 -  `* * * * * script.sh` *은 순서대로 min/hour/day/month/week(0-6,0:sunday)을 의미. 원하는 시간 설정
    * min에 */5 -> 매5분마다 같은식으로도 설정 가능
    * [Jenkins - use of H(hash syntax) in crontab 관련 글](https://issues.jenkins-ci.org/browse/JENKINS-17311) 
    * http://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EB%B0%98%EB%B3%B5_%EC%98%88%EC%95%BD%EC%9E%91%EC%97%85_cron,_crond,_crontab


## JavaScript

* 매번 까먹지만 boolean과 string, undefined의 타입체크와 변환에 주의하자  
    * `|`를 이용한 기본값 할당 불가. `this.value = value !== false` 식으로 처리
    * string|undefined로 넘어오는 값은 아예 `isActive !== 'false'` 이런식으로 처리하는것도 방법
* 배열의 아이템 삭제시 [].forEach 내부에서 [].splice를 쓰면 안된다.
    * [].filter를 쓸 것
    * Object[]일 경우 [].forEach(item => {delete item['whatever']})
    * https://gist.github.com/chad3814/2924672 
* 서버단에서 Object를 다룰때는 특히 주의하자. 개별 요청에서 전역에 참조되는 Object(어플리케이션 상태 등)를 변경하게 되면 모든 사용자에게 영향을 미친다. 
객체를 바로 참조하지 말고 항상 복사한 뒤 개별 컨텍스트 내에서 다루도록 하자.      


## ReactJS

* 컴포넌트 초기화 코드는 constructor 말고 componentDidMount에서 처리하자
    * 예를 들면 서버렌더링을 할 경우 초기화코드에서 window 객체를 참고하면 말없이 죽어버린다. 
    마운트 이후엔 참조 가능  
* 서버렌더링 코드를 구성할 때는 앱코드블럭(`<script src="app.js"></script>`)보다 
상태(`<script>window.__STATE__={/* state */}</script>`)를 먼저 선언해야 함을 잊지말자. 
위와 비슷하게 참조시점에 객체가 존재하지않아 문제 


## AngularJS

* 그냥 스타일가이드를 따르자
    * https://github.com/johnpapa/angular-styleguide
* config 에는 constants와 provider만 inject 가능
* AngularJS는 템플릿주석을 따로 지원하지 않는다. 별도 디렉티브를 만들던지 해야함. WTF
* Angular1에서는 es6 이전의 구린 js 문법을 보완하기 위해 몇가지 유틸이 존재한다. 
    * angular.copy
    * angular.forEach 등
    * https://docs.angularjs.org/api/ng/function
* `ng-if`와 `ng-show`의 차이는 엘리먼트를 아예 없애느냐 그냥 css로 노출여부만 제어하느냐의 차이
* `ng-if`는 `else`를 지원하지 않기 때문에 `ng-switch`를 이용하면 좋다
* `ng-repeat`에서 만든 참조는 해당 엘리먼트에서도 쓸 수 있음
    * ex) `<li ng-repeat="item in vm.items" class="{{item.className}}">{{item.text}}</li>`
* 반환하는 객체에 `$promise`가 있는 녀석들은 promise-like 하게 사용할 수 있다
    * ex) `getData().$promise.then(setProp1).then(setProp2UsingProp1);`   
* ui-router: 의존관계(parent-child)를 엮는건 주의해야 한다. state 변환시 params가 꼬일 수 있음
    * parent로부터 params을 상속받을 수 있지만 대부분의 경우 의존관계를 제거하고 명시적으로 params를 제어하는게 훨씬 낫다
    * 편집페이지 같은곳만 parent 고려해주고 나머진 root로 지정해 주면 좋을 듯
* ui-router: url을 처리할 때 `/`를 엄격하게 다룬다
    * optional하게 처리하고 싶다면 https://github.com/angular-ui/ui-router/wiki/Frequently-Asked-Questions#how-to-make-a-trailing-slash-optional-for-all-routes   


## CSS

* flexbox를 공부하자. 꽉 채운 레이아웃을 구성하기에 효과적. 그러니까, '앱'스런 레이아웃.
    * https://css-tricks.com/snippets/css/a-guide-to-flexbox/
    * https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties

## RSQL

* RSQL is a query language for parametrized filtering of entries in RESTful APIs
* https://github.com/jirutka/rsql-parser#grammar-and-semantic
* like matching에는 `*`을 쓰면 됨. ex) '바나나'로 시작-> `*바나나`


## Jenkins

* Build status 뱃지를 보여주려면 보안 설정에서 `Allow anonymous read access`를 체크해줘야함


## REST API

* cors 설정에서 클라이언트에서 받을 수 있는 헤더를 설정해 줄 수 있다. 네트워크탭에서 확인가능한 모든 정보를 기본적으로 제어할 수 있는건 아님


# Git

* 커밋의 날짜를 수정하고 싶으면 `--date` 옵션을 사용
    * 지금 시간으로 변경하고 싶다면 `git commit --amend --date="now"`
    * 또다른 방법으로는 `git commit --amend --reset-author --no-edit`


# Mail DM

* Daum 메일은 table 연관 태그들이 폰트관련 속성을 상속받지 못한다
* 아웃룩은 지옥이다. 기본적으로 이미지를 안보여주고 margin, padding 따위를 가볍게 무시하는 듯
* 의외로 font-family 셋팅이 먹는다