# AJAX 사용법 정리

* 웹 개발 초창기때에는 페이지의 일부분을 변경하기 위해서는 전체 페이지를 새로고침했어야 했습니다. AJAX는 페이지를 이동하지 않고도 일부분만 새로고침할 수 있는 방법입니다.
* 내 화면에서 일부분만 바뀐다는 건 AJAX 처리에서 아주 중요한 조건입니다. 서버에 파라미터를 넣어 보내면 DB에 접근하거나 값을 계산한 뒤에 자연스럽게 AJAX 콜백값으로 주게 되는데요. 이를 활용하여 내 화면을 수정하는 것이죠.
* 동기와 비동기 방식 차이
자바스크립트를 처리할 때 동기와 비동기 방식 처리를 잘 이해하고 만드는 것이 중요합니다. ​내가 어떤 처리를  순차적으로 처리할 때는 동기 방식을 사용해야 하고 ​하는 것마다 빨리 처리해야할 때는 비동기 방식을 사용해야 합니다.


> fetch
```fetch
fetch('http://example.com/data')
  .then(response => response.json()) // 응답을 JSON 형태로 변환
  .then(data => console.log(data)) // 데이터 처리
  .catch(error => console.error('Error:', error)); // 오류 처리
```

>> fetch option
```fetch
fetch('http://example.com/post', {
  method: 'POST', // HTTP 메소드 지정
  headers: {
    'Content-Type': 'application/json', // 콘텐츠 타입 설정
  },
  body: JSON.stringify({ key1: 'value1', key2: 'value2' }), // 요청 본문
})
.then(response => response.json())
.then(data => console.log('Success:', data))
.catch(error => console.error('Error:', error));
```

* fetch 방식의 ajax는 비교적 최근에 만들어졌습니다. 그렇기에 지원되지 않는 브라우저가 존재하며 이를 해결하려면 axios 혹은 jquery 를 사용하셔야 합니다.
* fetch는 Promise를 반환하므로, .then()과 .catch()를 사용하여 응답과 오류를 처리할 수 있습니다.


> Axios
``` axios
<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

axios.get('http://example.com/data')
  .then(response => console.log(response.data))
  .catch(error => console.error(error));

axios.post('http://example.com/post', { key1: 'value1', key2: 'value2' })
  .then(response => console.log(response.data))
  .catch(error => console.error(error));
```

* Axios 테스트 하기 위해 CDN 방식으로 진행. 실제 운영할 때는 직접 다운받아 include 할 것.

> jQuery
```
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.7.1/jquery.min.js"></script>

$.ajax({
  url: 'http://example.com/data',
  type: 'POST',
  data: JSON.stringify({
    param1: 'value1',
    param2: 'value2'
  }),
  contentType: 'application/json; charset=utf-8',
  dataType: 'json',
  success: function(data) {
    console.log('성공:', data);
  },
  error: function(error) {
    console.error('오류:', error);
  }
});

```

* 더이상 jQuery 는 사용하지 않음. 단지 레거시 코드로 어쩔 수 없이 사용해야 하는 경우 알아야 겠음. 