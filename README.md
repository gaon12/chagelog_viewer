> You can read to English!

## 변경사항 확인 프로그램

## 제작 의도

업데이트가 완료되면 어떤 점이 업데이트되었는지 확인하는 것이 있었으면 좋겠었습니다.

처음에는 텍스트문서를 열게 끔 하면 좋을 것 같았지만, 여러 스타일을 적용할 수 없고, 수정 사항이 있으면 수정본을 확인할 수 없습니다.

그렇기에 `iframe` 태그를 이용하여 서버에 있는 html을 불러오도록 하였습니다.

## 작동 원리

프로그램 버전 정보를 받으면(client\_version), 프로그램 버전이 이름인 html(filename\_extension) 파일을 서버(domain)에서 보여주는 방식입니다.

변수가 다음과 같이 설정되어 있다면…

```javascript
var client_version = "1.0.1";
var domain = "https://common.gaon.xyz/prj/MCD/changelog/";
var filename_extension = ".html";
```

[https://common.gaon.xyz/prj/MCD/changelog/1.0.1.html](https://common.gaon.xyz/prj/MCD/changelog/1.0.1.html) 페이지를 iframe으로 보여줍니다.

## 수정해야 하는 부분

html 파일은 총 3부분, 서버 설정도 수정해야 합니다.

### HTML 파일

#### 프로그램 버전

```javascript
var client_version
```

client\_version은 프로그램의 버전을 정의합니다. 버전 정의는 자유롭게 하면 됩니다. 버전 1, 버전 2 이런식으로 해도 되지만, 저는 1.0.1과 같은 형식을 권장합니다. 그러면 다음과 같이 수정해야 합니다.(아래의 예재는 1.3.5로 설정)

```javascript
var client_version = "1.3.5";
```

#### URL 주소

```javascript
var domain
```

파일이 존재하는 URL 주소를 정의합니다. URL 주소가 맞지만, 변수명은 domain입니다. 착각하지 말아주세요! 파일이 존재하는 디렉토리(폴더)까지 작성해 주세요. 그러면 다음과 같이 수정해야 합니다.

```javascript
var domain = "https://common.gaon.xyz/prj/MCD/changelog/";
```

#### 파일 확장자

```javascript
var filename_extension
```

파일의 확장자를 정의합니다. 기본값 그대로 두는것을 권장하지만, PHP나 JSP등 다른 언어로 작성하였다면 해당 확장자를 입력해 주세요. 텍스트파일도 가능합니다.

### 서버 설정

iframe 태그로 불러오면 대부분의 서버에서는 (크롬 기준) 연결을 거부한다는 메시지를 출력합니다. XSS 등 보안 문제를 방지하기 위해 서버에서 거부하는 것입니다. 하지만, 우리는 단순히 출력용으로만 사용하기에 XSS 등의 문제는 발생하지 않을 것입니다. 따라서 설정을 변경합니다.

#### 아파치(httpd)

반드시! domain에 해당하는 폴더에서 .htaccess를 다음과 같이 설정합니다.

도메인 루트 폴더에서 적용할 경우, 큰 보안 문제가 발생할 수 있습니다.

`Header set X-Frame-Options ALLOW`

#### 엔진엑스(nginx)

`add\_header X-Frame-Options ALLOW;`

엔진엑스는 반드시 changelog 전용 도메인을 생성하고, changelog용으로만 사용하는것을 매우 권장합니다. 엔진엑스는 아파치와 달리 .htaccess로 폴더별 관리할 수 없고, 폴더별 관리하기에는 복잡하기 때문입니다.

## 라이선스

라이선스는 MIT 라이선스를 선택했습니다. 따라서 본 저장소의 주소만 적어만 주신다면 지지고 볶든 상관 안합니다.

## 버그가 발생했나요?

이슈 탭을 통해 버그를 알려주세요!

## Changelog Viewer

## Production intention

When the update is complete, I wanted to check what was updated.

At first, I thought it would be nice to open a text document, but I can't apply multiple styles, and if there are any modifications, I can't check the revision.

Therefore, I used the `iframe` tag to load the HTML on the server.

## Principles of Operation

When the program version information is received (client\_version), the html(filename\_extension) file whose name is the program version is displayed on the server (domain).

If the variable is set to...

```javascript
var client_version = "1.0.1";
var domain = "https://common.gaon.xyz/prj/MCD/changelog/";
var filename_extension = ".html";
```

https://common.gaon.xyz/prj/MCD/changelog/1.0.1.html shows the page as an iframe.

## The part that needs to be corrected

The HTML file is a total of three parts, and the server settings need to be modified.

### HTML File

#### Program's Version

```javascript
var client_version
```

client\_version defines the version of the program. You can define the version freely. You can do it like version 1, version 2, but I recommend the same format as 1.0.1. This should be corrected as follows (the example below is set to 1.3.5).

```javascript
var client_version = "1.3.5";
```

#### URL Address

```javascript
var domain
```

Define the URL address where the file exists. The URL address is correct, but the variable name is domain. Please don't get me wrong! Please write to the directory (folder) where the file exists. Then you need to modify it like this:

```javascript
var domain = "https://common.gaon.xyz/prj/MCD/changelog/";
```

#### File Extension

```javascript
var filename_extension
```

Defines the extension of the file. It is recommended to leave the default value, but if you have written it in a different language, such as PHP or JSP, please enter the appropriate extension. Text files are also available.

### Server Settings

When loaded with the iframe tag, most servers output a message that they refuse to connect (based on chrome). The server rejects it to prevent security issues such as XSS. However, we use it simply for output, so there will be no problems such as XSS. Therefore, change the settings.

#### Apache2(httpd)

Make sure to set .htaccess in the folder corresponding to the domain as follows:

Applying from the Domain Root folder can cause major security issues.

`Header set X-Frame-Options ALLOW`

#### Nginx

`add\_header X-Frame-Options ALLOW;`

It is highly recommended that Nginx create a domain dedicated to changelog and use it only for changelog. Unlike Apache2, Nginx cannot be managed by folder with .htaccess, and it is complicated to manage by folder.

## License

For licenses, I selected MIT licenses. Therefore, as long as you write down the address of this repository, I don't care if you use this code.

## Do you find a bug?

Please report bugs through the Issues tab!
