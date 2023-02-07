---
layout: post
author: "Hayeon"
title:  "웹 크롤링을 통한 유해 사이트 자동 탐지 프로젝트"
subtitle: "판별률 97% 달성을 통해 유해 사이트 차단에 기여"
type: "Python"
projects: true
text: true
portfolio: true
main-img: "img/crawling.png"
role-title: "Developer"
team: "PM & Developer 1명, Developer 4명"
platforms: "Ubuntu 18.04.5 LTS"
date: "Jul 2020 - Dec 2021"
order: 1
---

# Overview

석사 과정 중 불법 웹툰, TV, 성인물과 관련된 불법 사이트의 링크를 모아두는 링크 모음 사이트를 크롤링하여 유해 사이트를 자동으로 탐지하는 시스템을 개발했습니다.
링크 모음 사이트를 기반으로 유해 사이트를 수집한 뒤에 HTML, URL을 기반으로 카테고리를 분류하고 관련 정보를 다음과 같이 데이터베이스에 축적하였습니다.
<br>
<br>

![image](https://user-images.githubusercontent.com/77316808/199218907-2a2a8676-b2d2-4cfd-afbb-6662560f0029.png){: width="70%" height="70%"}{: .align-center}
<br>
<br>

## 유해 사이트 현황

유해 사이트는 날이 갈수록 많아지는 추세입니다. 유해 사이트에는 웹툰, TV 프로그램, 성인물 등 다양한 사이트가 있습니다. 그 중에서도 돈을 내고 유료로 이용해야 하는 웹툰을 불법 복제한 사이트의 경우 웹툰 산업에 심각한 피해를 주고 있습니다.
<br>
<br>

![image](https://user-images.githubusercontent.com/77316808/199217798-ebdf4b1c-d78b-4a4c-89f0-f1945ca1ba62.png)
<br>

실제로 불법 웹툰 사이트의 접근이 쉬워지면서 기존 웹툰 사이트의 트래픽을 넘어서고 있습니다. 국내 웹툰 시장 규모는 7000억원 정도인데 업계의 피해액이 시장 규모의 30% 정도에 이를 정도로 심각한 수준입니다.
따라서 이러한 사이트들을 자동으로 탐지하여 신고할 목적으로 시스템을 개발했습니다.
<br>
<br>
<br>

---
## 웹 크롤링 시스템 설명

웹 크롤링 시스템은 링크 모음 사이트를 seeds로 불법 사이트를 수집한 뒤 카테고리를 분류하고 ip, 국가 등 관련 정보를 축적하였습니다.
유해 사이트를 수집할 때에는 `Requests`, `BeautifulSoup` 라이브러리를 이용했습니다.
<br>
<br>

### ✔️ Requests

Requests 라이브러리는 python에서 특정 웹사이트에 HTTP 요청을 보내 HTML 문서를 받아올 수 있는 라이브러리이며 기본적으로 아래와 같이 요청합니다.<br>
`res = requests.get(url)`

<br>
크롤링을 할 때 서버에서 봇으로 인지하고 차단하는 경우가 있기 때문에 HTTP 헤더에 운영체제와 웹 브라우저 정보 등을 포함하는 User-Agent 정보를 입력해야 합니다. 이러한 정보가 없으면 서버에서 비정상적인 접속 시도로 간주하여 접속이 차단됩니다.
<br>
<br>

### ✔️ BeautifulSoup

BeautifulSoup 라이브러리는 Requests로 얻는 HTML 정보에서 원하는 데이터를 가져오기 쉽게 비슷한 분류의 데이터별로 나누어주는 라이브러리입니다.<br>
`<p>`태그로 감싸져 있는 부분을 찾는다면 아래와 같이 찾을 수 있습니다.<br>
`p = bs.find('p')`
<br>
<br>
<br>

---
## 데이터베이스 수집 구조

유해 사이트의 기본 정보, 운영자 정보, 접속 가능 여부, SNS 정보, 유해 사이트 운영 형태로 총 5개의 테이블로 구성하였습니다.
<br>
<br>

### 1️⃣ 유해 사이트의 기본 정보
<br>

![image](https://user-images.githubusercontent.com/77316808/199218907-2a2a8676-b2d2-4cfd-afbb-6662560f0029.png){: width="70%" height="70%"}{: .align-center}

유해 사이트의 기본 정보에는 `url`과 `제목`, `카테고리`, `HTML 저장 경로` 등 유해 사이트를 식별하기 위한 기본 정보들을 저장했습니다.
<br>
<br>
<br>

### 2️⃣ 유해 사이트의 운영자 정보
<br>

![image](https://user-images.githubusercontent.com/77316808/199224338-09b3c7ee-4ad7-46ed-a629-a61bea4acfd6.png){: width="70%" height="70%"}{: .align-center}

유해 사이트의 `ip`와 `Google Analytics ID`를 수집하고 유해 사이트가 이용하는 `CMS`(Content Management System)가 그누보드인지 제로보드인지 파악하여 운영자 추적이나 유해 사이트 운영 그룹 특정에 도움이 될 만한 정보를 저장했습니다.
<br>
<br>
<br>

### 3️⃣ 유해 사이트의 접속 가능 여부
<br>

![image](https://user-images.githubusercontent.com/77316808/199224836-d2237f2d-a24c-4e67-a754-dbf5612c7acd.png){: width="70%" height="70%"}{: .align-center}

웹 크롤링 시스템이 유해 사이트 url을 `수집한 날짜`와 수집한 유해 사이트를 마지막으로 `방문한 날짜`가 저장되어 있어서 해당 유해 사이트 접속이 언제까지 가능했는지 확인할 수 있습니다.
<br>
<br>
<br>

### 4️⃣ 유해 사이트의 SNS 정보
<br>

![image](https://user-images.githubusercontent.com/77316808/199225145-2cde024c-500b-4fd1-a0de-49c0bcf7da6f.png){: width="70%" height="70%"}{: .align-center}

유해 사이트에서 운영하는 `트위터`와 `텔레그램` 주소를 수집하고 각 SNS에서 유해 사이트 url을 포함하고 있는 메시지를 추출하여 저장했습니다.
<br>
<br>
<br>

### 5️⃣ 유해 사이트의 운영 형태
<br>

![image](https://user-images.githubusercontent.com/77316808/199226196-914d67cc-7e13-49f9-a2c4-92c5f3682307.png){: width="70%" height="70%"}{: .align-center}

유해 사이트의 ip를 기반으로 `whois` 정보와 `VPN` 및 `CDN` 사용 여부를 확인하였습니다. 추적이나 단속을 피하기 위해 운영 서버를 해외에 두거나, VPN 또는 CDN 서비스를 사용하는 유해 사이트가 다수 존재하는 것을 확인할 수 있었습니다.
<br>
<br>
<br>
<br>

---
## 유해 사이트 수집 결과

웹 크롤링 시스템을 이용하여 수집된 총 7,083개 url 중에서 접속 가능한 url은 628개이며 유해 사이트는 610개, 정상 사이트는 18개로 97%의 판별률을 보였습니다. 수집된 url에 비해 접속 가능한 url이 적은 이유는 유해 사이트가 단속을 회피할 목적으로 url을 주기적으로 변경하기 때문입니다.

따라서 해당 시스템을 바탕으로 현재 방송통신심의위원회의 차단 심의에 기여하였고, 지속적인 유해 사이트 차단을 위한 효과적인 정책 수립에 도움을 줄 수 있습니다.