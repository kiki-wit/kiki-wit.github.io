---
date: 2025-09-14 11:48
layout: post
title: 개발환경
subtitle: 터미널, 쉘, 패키지 관리자, Git 등 차이와 역할
description: OS별 개발 환경 및 소프트웨어 종류, 설치 방법에 대해 정리
image: 
optimized_image: https://res.cloudinary.com/dm7h7e8xj/image/upload/c_scale,w_380/v1559820489/js-code_n83m7a.jpg
category: 개발환경
tags:
  - SETTING
author: kiki
---

처음 운영체제 위에 개발 환경을 구축할 때는 여러 소프트웨어와 프로그램을 설치해야 한다. 이 과정에서 터미널을 사용하면 소프트웨어 설치를 보다 효율적으로 진행할 수 있다. 다만, 윈도우, 맥, 리눅스 등 운영체제 종류에 따라 설치 방법이 다르기 때문에 주의가 필요하다. 또한, 개발 환경 구성 방식에 따라 업무 효율이 크게 달라질 수 있으므로, 이를 쉽게 구성하고 관리할 수 있는 방법을 정리하고자 한다.


# 환경 구성

## 명령어

**터미널(Terminal)**은 사용자가 명령어(CLI)를 통해 운영체제에 명령을 전달하고, 그 결과를 확인할 수 있는 **입출력 창(UI)**이다. 쉘이 있어야 명령어가 실행되며, 쉘이 없으면 단순 입력창이 불과하다. command나 shell script를 입력하여 다양한 작업을 수행할 수 있다.
<br/>
**쉘(Shell)**은 터미널 내부에서 실행되는 소프트웨어로, 사용자가 입력한 명령어를 해석하여 커널에 전달하는 역할을 한다. 대표적인 쉘로는 zsh, bash, fish 등이 있으며, 터미널 환경 개선과 사용자 경험(UI/UX)을 고려해 개발된 iTerm2, Warp 같은 소프트웨어와 함께 사용할 수 있다.
<br/>
또한 macOS에서는 Homebrew를 통해 프로그램 설치, 업데이트, 삭제를 손쉽게 관리할 수 있다. Homebrew는 개발 환경 구성과 유지 관리를 편리하게 해주는 **패키지 관리자(package manager)**다.

터미널(iTerm2, Terminal.app) <br/>
   └── 쉘(zsh, bash, fish) <br/>
          └── 명령어(CLI) 실행

#### 개념 레이어

<table>
  <thead>
    <tr>
      <th>레이어</th>
      <th>예시</th>
      <th>역할 / 설명</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>터미널</td>
      <td>macOS: Terminal.app, iTerm2, Warp / Windows: CMD, PowerShell, Windows Terminal</td>
      <td>사용자가 명령어를 입력하고 결과를 확인할 수 있는 창 / UI</td>
    </tr>
    <tr>
      <td>쉘(shell)</td>
      <td>bash (Bourne Again Shell), zsh (Z Shell, bash보다 기능 많음), fish (사용자 친화적, 예쁘게 꾸며진 쉘)</td>
      <td>명령어를 해석하고 실행하는 프로그램</td>
    </tr>
    <tr>
      <td>명령어(command)</td>
      <td>ls, cd, ruby -v, brew install ruby</td>
      <td>쉘에서 실행되는 실제 명령어</td>
    </tr>
    <tr>
      <td>패키지 관리자(package manager)</td>
      <td>Homebrew, Chocolatey, apt, yum</td>
      <td>프로그램 설치 / 업데이트 / 삭제를 편리하게 해주는 도구</td>
    </tr>
    <tr>
      <td>언어 / 개발 환경</td>
      <td>Ruby, Node.js, Python</td>
      <td>개발용 언어 및 실행 환경</td>
    </tr>
    <tr>
      <td>버전 관리 도구</td>
      <td>rbenv, pyenv, nvm</td>
      <td>특정 언어 버전을 관리하고 쉽게 전환할 수 있는 도구</td>
    </tr>
  </tbody>
</table>

- **To bold text**, use `<strong>`.
- *To italicize text*, use `<em>`.
- Abbreviations, like <abbr title="HyperText Markup Langage">HTML</abbr> should use `<abbr>`, with an optional `title` attribute for the full phrase.
- Citations, like <cite>&mdash; Thomas A. Anderson</cite>, should use `<cite>`.
- <del>Deleted</del> text should use `<del>` and <ins>inserted</ins> text should use `<ins>`.
- Superscript <sup>text</sup> uses `<sup>` and subscript <sub>text</sub> uses `<sub>`.

Most of these elements are styled by browsers with few modifications on our part.

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

Vivamus sagittis lacus vel augue rutrum faucibus dolor auctor. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Morbi leo risus, porta ac consectetur ac, vestibulum at eros.

## Code

Cum sociis natoque penatibus et magnis dis `code element` montes, nascetur ridiculus mus.

```js
// Example can be run directly in your JavaScript console

// Create a function that takes two arguments and returns the sum of those arguments
var adder = new Function("a", "b", "return a + b");

// Call the function
adder(2, 6);
// > 8
```

Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa.

## Lists

Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Aenean lacinia bibendum nulla sed consectetur. Etiam porta sem malesuada magna mollis euismod. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.

* Praesent commodo cursus magna, vel scelerisque nisl consectetur et.
* Donec id elit non mi porta gravida at eget metus.
* Nulla vitae elit libero, a pharetra augue.

Donec ullamcorper nulla non metus auctor fringilla. Nulla vitae elit libero, a pharetra augue.

1. Vestibulum id ligula porta felis euismod semper.
2. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus.
3. Maecenas sed diam eget risus varius blandit sit amet non magna.

Cras mattis consectetur purus sit amet fermentum. Sed posuere consectetur est at lobortis.

Integer posuere erat a ante venenatis dapibus posuere velit aliquet. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Nullam quis risus eget urna mollis ornare vel eu leo.

## Images

Quisque consequat sapien eget quam rhoncus, sit amet laoreet diam tempus. Aliquam aliquam metus erat, a pulvinar turpis suscipit at.

![placeholder](https://placehold.it/800x400 "Large example image")
![placeholder](https://placehold.it/400x200 "Medium example image")
![placeholder](https://placehold.it/200x200 "Small example image")



Nullam id dolor id nibh ultricies vehicula ut id elit. Sed posuere consectetur est at lobortis. Nullam quis risus eget urna mollis ornare vel eu leo.










