---
layout: post
author: "Hayeon"
title:  "Mac m1 Monterey 개발 환경 설정하기"
subtitle: "맥북 개발환경 Homebrew, iTerm2, oh-my-zsh, 플러그인 등 초기 설정"
type: "Mac M1"
text: true
blog: true
post-header: true
header-img: "img/macpro.jpg"
order: 1
---
맥북으로 바꾸면서 맥북 관련 포스팅을 찾아보는데 자동 완성, 터미널 등 다양한 개발 환경 설정이 가능한 것을 보고 찾아서 정리하게 되었다. 이 글을 통해 macOS에서 터미널을 자주 사용하는 개발자들이 깔끔한 테마 위주의 개발 환경을 설정하는 데에 도움이 되면 좋겠다.
<br>

![image](https://user-images.githubusercontent.com/77316808/164450030-e3013db5-78b1-421f-86e5-52022db8b4a7.png){: width="70%" height="70%"}{: .align-center}
<br>

# 필수 프로그램

## Homebrew
<br>

![image](https://user-images.githubusercontent.com/77316808/164458776-e2c3511a-cf70-4574-a70d-4b62670f08ba.png){: width="70%" height="70%"}{: .align-center}

<br>

[Homebrew](https://brew.sh)는 각종 커맨드라인 프로그램과 일반 프로그램을 손쉽게 설치해주는 맥용 패키지 매니저이다. 리눅스의 `apt`와 비슷하며, 손쉽게 설치할 수 있고 관리도 간단하다.
<br>
<br>

### 설치

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"`
<br>
<br>

### 설치 확인

`brew -v`
<br>
<br>
<br>

### Homebrew 명령어 정리

brew [명령어 문서](https://docs.brew.sh/Manpage.html)는 다음과 같이 잘 설명되어 있고, 그 중에서 자주 쓰이는 기본 명령어를 정리했다.
<br>
<br>

#### 명령어
- `brew update` : brew를 최신 버전으로 업데이트
- `brew search <패키지명>` : 프로그램이 있는지 검색
- `brew install <패키지명>` : 프로그램 설치
- `brew list` : 설치된 패키지 list 확인
- `brew info <패키지명>` : 패키지 정보 보기
- `brew upgrade` : 모든 패키지 업그레이드
<br>
<br>
<br>

## Xcode

![image](https://user-images.githubusercontent.com/77316808/164459056-1a30a326-58c4-4d9c-8574-4417668e7b94.png){: width="70%" height="70%"}{: .align-center}

macOS는 명령어 도구를 별도로 설치해야 한다. 예전에는 [Xcode](https://developer.apple.com/xcode/)를 전체 설치하고 추가로 명령어 도구를 설치해야 했으나 현재는 명령어 도구만 따로 설치할 수 있다.<br>

위에 설명했던 homebrew를 설치하면 자동으로 Xcode 명령어 도구를 설치하기 때문에 따로 설치하지 않아도 된다.
<br>

### 설치

`xcode-select --install`
<br>
<br>
<br>

# 터미널 설정

## iTerm2

macOS에 기본으로 설치되어 있는 Terminal도 편리하지만, 기존보다 다양한 플러그인과 테마를 통해 개발을 수월하게 해주는 iTerm2를 터미널로 사용하려고 한다.
iTerm2는 검색, 복사 등 다양한 기능이 있고 쉽게 테마를 설정할 수 있어서 많이 사용한다.
<br>
<br>

### 설치

위에서 설치한 brew로 설치하는 방법과 [여기](https://iterm2.com/downloads.html)를 클릭해서 직접 다운로드하는 방법 중 편한 방법으로 다운로드하면 된다.

`brew cask install iterm2`
<br>
<br>
<br>

### 테마 선택
<br>

![image](https://user-images.githubusercontent.com/77316808/164455045-7fd11001-9f37-4db0-b287-456439974708.png){: width="70%" height="70%"}{: .align-center}
<br>

설치를 완료했으면 [iTerm2 테마](https://iterm2colorschemes.com)를 둘러보고 마음에 드는 테마를 선택하면 된다. 셀 수 없을 정도로 다양한 테마가 있는데 난 뚜렷하고 팔레트가 이쁜 dracula 테마로 골랐다.

다운로드 받은 파일의 확장자인 .text를 지우면 자동으로 .itermcolors로 변경된다.
변경하고 파일을 더블클릭하면 자동으로 `iTerm Color Preset`에 추가된다.
<br>
<br>

### 테마 적용

위의 과정까지 완료했다면, iTerm2를 실행하고 설정(`⌘` + `,`)창에서 `Profiles` 창의 `Colors` 탭에서 오른쪽 하단의 `Color Presets`를 클릭한다.

![image](https://user-images.githubusercontent.com/77316808/164503791-915a3073-9860-4725-a5d8-c2e29b01b960.png){: width="70%" height="70%"}{: .align-center}

빨간색 체크 박스에서 방금 전에 추가한 `dracula+` 프리셋을 선택할 수 있다.
<br>
<br>

### 한글파일 깨짐방지
<br>

![image](https://user-images.githubusercontent.com/77316808/164504081-39cc1c3a-9c73-4179-abd1-bac2ce257548.png){: width="70%" height="70%"}{: .align-center}

한글파일의 파일명의 자음 모음이 분리되는 현상을 방지하는 설정도 해주었다.
- Unicode 설정
  - `Profiles` > `Text` > `Unicode normalization form` : `NFC`

<br>

### 상태바 추가
<br>

![image](https://user-images.githubusercontent.com/77316808/164493159-03b7cdb7-eb78-4a8d-99cf-9f8b73b25784.png){: width="60%" height="60%"}{: .align-center}
<br>

iTerm2에 새롭게 추가된 상태바 기능이다. 원하는 위치에 상태바를 추가하고 여러가지 정보를 선택해서 볼 수 있다.

![image](https://user-images.githubusercontent.com/77316808/164504266-2e74d898-1bac-4b26-914d-9006ca0d89c2.png){: width="70%" height="70%"}{: .align-center}

- 상태바 추가
  - `Profile` > `Session` : Status bar enabled 체크
  - `Configure Status Bar` 선택하여 원하는 항목 추가
<br>
<br>
<br>

## oh-my-zsh

iTerm2를 설치하고 테마도 적용했으니 쉘을 바꾸어 보았다. macOS는 기본적으로 zsh를 사용하고 있다. zsh의 관리 프레임워크인 oh-my-zsh를 사용하여 테마를 적용하고 여러 플러그인을 설치하려고 한다.
<br>

### 설치

zsh을 최신 버전으로 업데이트하고 zsh를 위한 추가적인 자동완성 [zsh-completions](https://github.com/zsh-users/zsh-completions)도 설치한다.

`brew install zsh zsh-completions`

<br>

zsh의 설정을 관리해주는 oh-my-zsh를 설치한다.

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
<br>
<br>

### 플러그인

oh-my-zsh의 강력한 점은 플러그인이다. 나는 명령어를 하이라이트하는 플러그인 [zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting)과 자동완성하는 플러그인 [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)을 설치했다.
<br>

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
<br>

```
git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
```
<br>

플러그인을 설치하면 반드시 `~/.zshrc`파일에 설정해야 한다. `vim ~/.zshrc` 명령어를 통해 파일을 열어 `plugin` 항목에 플러그인을 다음과 같이 추가한다.

<script src="https://gist.github.com/gkduss/038a786f90842a4d84b5cc7d4ec32739.js"></script>
<br>

추가 후 `source ~/.zshrc` 명령어를 실행하여 설정을 불러와야 한다. 설정을 불러오면 존재하지 않는 명령어를 입력할 때 빨간색으로 뜨는 것을 확인할 수 있다.
<br>
<br>

#### fzf

[fzf](https://github.com/junegunn/fzf)는 원하는 파일이나 히스토리를 쉽고 빠르게 찾을 수 있도록 도와주는 플러그인이다. 설치는 brew를 통한 다음 명령어로 간편하게 할 수 있다.
`brew install fzf`
<br>

설치가 완료되었으면 앞에 말했던 것처럼 `~/.zshrc` 파일을 열어 `plugin` 항목 마지막줄에 `fzf`를 추가하고 `source ~/.zshrc`를 통해 설정을 불러온다.<br>

정말 다양한 기능이 있지만 가장 많이 쓰이는 기능만 간단히 정리했다.
<br>
<br>

#### 단축키
- `ctrl + T` : 하위 디렉토리 파일 검색
- `ctrl + R` : 히스토리 검색
- `esc` : 취소

<br>
<br>