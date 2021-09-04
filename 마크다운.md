마크다운은 어떻게 사용할까?
===
마크다운 문법을 알아보자.
---

### 1. 제목
* `<h1>` 
    ```Markdown
    작성하고 싶은 제목
    ===
    ('=' 3개 이상 작성)

    또는

    # 작성하고 싶은 제목
    ```

    * `<h2>`
    ```Markdown
    작성하고 싶은 제목
    ---
    ('-' 3개 이상 작성)

    또는

    ## 작성하고 싶은 제목
    ```

* `<h3>` ~ `<h6>`
    ```Markdown
    ### 작성하고 싶은 제목 (h3)
    #### 작성하고 싶은 제목 (h4)
    ##### 작성하고 싶은 제목 (h5)
    ###### 작성하고 싶은 제목 (h6)
    ```

### 2. 스타일
* `<i>` `<em>` (이탤릭체)
    ```Markdown
    *기울이고 싶은 문장*

    또는

    _기울이고 싶은 문장_
    ```

* `<b>` `<strong>` (두껍게)
    ```Markdown
    **두껍게 하고 싶은 문장**

    또는

    __두껍게 하고 싶은 문장__
    ```

* `<s>` `<del>` (취소선)
    ```Markdown
    ~~취소선을 긋고 싶은 문장~~
    ```

* `<u>` `<ins>` (밑줄)
    ```Markdown
    <u>밑줄</u>
    ```

### 3. 목록
* `<ol>` (순서가 있는 목록)
    ```Markdown
    1. 순서가 있는 목록
    2. 순서가 있는 목록
    3. 순서가 있는 목록

    또는 

    1. 순서가 있는 목록
    1. 순서가 있는 목록
    1. 순서가 있는 목록
    ```

* `<ul>` (순서가 없는 목록)
    ```Markdown
    - 순서가 없는 목록
    * 순서가 없는 목록
    + 순서가 없는 목록
    ```

### 4. 링크
* `<a>`
  * 방법 1: 
    ```Markdown
    [text](href "title")

    예) 
    [구글 바로가기] https://google.com "구글로 가는 링크입니다."
    ```
    text - 링크 버튼 텍스트<br />
    href - 링크할 URL 주소<br />
    title - 마우스 오버시 추가 정보를 제공하는 텍스트 (생략 가능)<br />

  * 방법 2

    ```Markdown
    [text][reference]
    [reference]: href "title"

    예) 
    [구글 바로가기][google link]

    [google link]: https://google.com "구글로 가는 링크입니다."
    ```
    reference - 링크에 대한 참조<br />

### 5. 이미지
* `<img>`
    ```Markdown
    ![alt](src "title")

    예)
    ![깃허브 로고](https://github.githubassets.com/images/modules/logos_page/GitHub-Mark.png "깃허브 공식 로고 입니다.")
    ```
    alt - 이미지 대체 텍스트<br />
    src - 이미지 경로<br />
    title - 마우스 오버시 추가정보를 제공하는 텍스트 (생략 가능)<br />

### 6. 코드
* `<code>` (인라인)
    ```Markdown
    `코드`
    ```
* `<pre>` (블록)
    ```markDown
        ```type
        content
        ```
        ('`' 3개 이상 작성)

        예)
        ```HTML
        <div>
            <p>Hello, World!</p>
        <div>
        ```
    ```
    type - 코드의 타입 (HTML, Markdown, css, javascript, ...)<br />
    content - 코드 내용<br />

### 7.표
* `<table>` `<th>` `<td>`
    ```Markdown
    | 제목1 | 제목2 | 제목3 |
    | :--- | :---: | ---: |
    | 값 1 | 값 2 | 값 3 |

    (`-` 3개 이상 작성)
    ```
    | :--- | - 왼쪽 정렬<br />
    | :---: | - 가운데 정렬<br />
    | ---: | - 오른쪽 정렬<br />

### 8. 인용문
* `<blockquote>`
    ```Markdown
    > 인용문
    >> 중첩된인용문
    ```

### 9. 수평선
* `<hr>`
    ```Markdown
    ---

    ***

    ___

    (각각 3개 이상 작성)
    ```

### 10. 줄 바꿈
* `<br>`
    ```
    <br>
    ```
    띄어쓰기 2번도 줄 바꿈 되지만, 가독성이 떨어지니 `<br>` 태그를 쓰자

### 11. 주석
* `<!-- -->`
    ```Markup
    <!--주석 내용-->
    ```

### 12. 각주
* `<q>` `<site>`
    ```Markup
        신은 죽었다. <sup id="footnote">[1](#description)</sup>

        <a id="description">[1](#footnote)</a>: 니체가 남긴 말이다.  
    ```
    기존 마크다운은 각주기능을 제공하지 않는다. 하지만 HTML을 사용하면 확장없이도 구현이 가능하다.