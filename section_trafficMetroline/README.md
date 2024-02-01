## 지하철 섹션
지하철 노선도 관련된 이미지를 등록하는 위치입니다.  
이미지 작업이 끝난 후에는, common > src 경로에 파일을 복사해주세요.

## 기능 명세
### 지하철 노선도 :
- [x] 이미지 리소스 확보 (1/12)  - 이지우
 예시 이미지
![1호선](https://mblogthumb-phinf.pstatic.net/20150627_37/revolutio419_1435375888142XpTtP_PNG/LINE_1.png?type=w420)
- [x] 애니메이션 슬라이드 초안 (1/12) - 박원빈
  
- [x] 오른쪽으로 이미지 이동 버튼 구현 (1/12) - 박원빈 (예시코드)
 ```js
var traffic_slide_gallery_Xoffset = 0;
var intervalId = null;
const TRAFFIC_IMAGE_WIDTH= 600

function traffic_Move() {
    traffic_slide_gallery_Xoffset -= TRAFFIC_IMAGE_WIDTH
    if (traffic_slide_gallery_Xoffset < -8*TRAFFIC_IMAGE_WIDTH) {
        traffic_slide_gallery_Xoffset = 0
    }
    $('#traffic_slide_gallery').animate({'marginLeft': `${traffic_slide_gallery_Xoffset}px`}, 300)
}
```

- [x] 왼쪽으로 이미지 이동 버튼 구현 (1/15) - 이지우

```js
function traffic_back() {
    traffic_slide_gallery_Xoffset += TRAFFIC_IMAGE_WIDTH
    if (traffic_slide_gallery_Xoffset > 0) {
        traffic_slide_gallery_Xoffset = -8*TRAFFIC_IMAGE_WIDTH
    }
    $(`#traffic_slide_gallery`).animate({'marginLeft': `${traffic_slide_gallery_Xoffset}px`}, 300)
}
```

- [x] 자동넘기기 활성화 되면 중지 버튼으로 기능 변경(재생/중지 기능버튼 일체화) (1/16) - 박원빈

```js
function traffic_play() {
    // setInterval의 ID를 저장하고 반환
    if (intervalId === null) {
        intervalId = setInterval(traffic_Move, 1000);
        $('#traffic_playToggle').text('■')
        $('#traffic_playToggle').addClass('BigChar')
    } else {
        clearInterval(intervalId);
        intervalId = null
        $('#traffic_playToggle').removeClass('BigChar')
        $('#traffic_playToggle').text('▶')
    }
}
```

- [x] 각종 버튼과 이미지에 대한 CSS 설정 - 박원빈 (1/16)

### 지하철 길찾기
- [x] 네이버 지하철 URL 페턴 분석 (1/15) - 박원빈
  - https://map.naver.com/p/subway/{수도권}/{출발역}/{도착역}/{경유역}
- [x] 각 조원들이 자주 사용하는 지하철역 조사

| 이름  | 코드   |
|-----|------|
| 선택안함 | - |
| 수도권 | 1000 |
| 구로디지털단지 | 172,746 | 
| 홍대 | 239,4003,1609|
| 석남 | 20212 |

- [x] 길찾기 링크 생성 (1/15) - 박원빈  
예시 : 수도권 : 홍대 -> 구로디지털단지, 경유역 선택안함
https://map.naver.com/p/subway/1000/239,4003,1609/172,746/-

![image](https://github.com/ParkWonBin/Codelabit_AICC_Project_01/assets/153358246/0f445b42-1c3f-492a-b4c9-676fd984b8d6)

- [x] 기능구현
