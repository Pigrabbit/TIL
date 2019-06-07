# Responsive Design

다양한 기기에서(desktop, tablet and phone) web browser를 이용할 수 있게 됨에 따라 각 기기에 따라 다른 화면을 보여주어야 하는 필요성이 생겼다.
HTML, CSS를 이용해서 responsive design을 한다면 각각의 device에서 보기 좋은 화면을 제작할 수 있다.

## Viewport

Viewport란 user에게 보이는 web page 영역을 말한다.
이는 각 기기마다 다르며, 당연하게 desktop보다 phone에서 더 작다.

HTML5에서는 `<meta>` 태그를 이용해 viewport를 설정할 수 있다.

``` html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

content중 width에서는 웹 페이지의 width를 기기의 width 에 맞추며, initial-scale에서는 초기 zoom level을 설정한다.

## Media queries

CSS3에서 `@media` rule을 이용해 styling을 특정 조건에 따라 적용시킬 수 있다.

``` css
@media only screen and (min-width: 768px) {
	flex-direction: row;
}
```

위의 코드에서 browser windoe가 768px 보다 크거나 같을 때, flex-direction이 row로 적용된다.

Mobile 화면부터 디자인을 하고 media query의 min-width를 사용하면서 device 별 styling을 적용시키는 방법이 선호된다.
일반적으로 moblie-->tablet, tablet-->desktop의 두 개의 breakpoint를 두고 design한다.
typical device breakpoint들은 아래와 같다.

``` css
/* Extra small devices (phones, 600px and down) */
@media only screen and (max-width: 600px) {...} 

/* Small devices (portrait tablets and large phones, 600px and up) */
@media only screen and (min-width: 600px) {...} 

/* Medium devices (landscape tablets, 768px and up) */
@media only screen and (min-width: 768px) {...} 

/* Large devices (laptops/desktops, 992px and up) */
@media only screen and (min-width: 992px) {...} 

/* Extra large devices (large laptops and desktops, 1200px and up) */
@media only screen and (min-width: 1200px) {...}
```

