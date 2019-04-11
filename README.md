# Smooth as Butter: Achieving 60 FPS Animations with CSS3

### Nguồn:  [Medium](https://medium.com/outsystems-experts/how-to-achieve-60-fps-animations-with-css3-db7b98610108)

<div style="display: flex; justify-content: center; padding: 20px"><video id="embedlyVideo_html5_api" class="vjs-tech" preload="none" poster="https://thumbs.gfycat.com/ThankfulContentCoypu-size_restricted.gif" loop="" src="https://thumbs.gfycat.com/ThankfulContentCoypu-mobile.mp4"><source src="https://thumbs.gfycat.com/ThankfulContentCoypu-mobile.mp4" type="video/mp4"></video></div>

Việc tạo ra các thành phần Animation, hay chính là **Hoạt cảnh** ở trên các ứng dụng di động của bạn là rất dễ dàng. Chính xác là như vậy nếu bạn làm theo các mẹo mà chúng tôi đưa ra dưới đây.

Trong khi tất cả mọi người đang sử dụng các Animation CSS3 trên các thiết bị di động ngày nay, rất nhiều người đã không làm việc đó đúng cách. Có những thực tế tốt nhất cho thấy điều đó diễn ra liên tục và không thực sự được chú ý đến. Điều này diễn ra chủ yếu bởi vẫn còn những người chưa thực sự hiểu bản chất tại sao những thực tế đó vẫn tồn tại và được chứng minh một cách mạnh mẽ như vậy.

Ngày nay, các thiết bị với những thông số kỹ thuật trải dài trên một phổ lớn như vậy, nếu bạn không tối ưu hóa code của mình để xem xét đến điều này, thay vì những Animation hoạt động một cách mượt mà, sau cùng bạn sẽ mang lại một trải nghiệm dưới mong đợi với lượt chia sẻ cao nhất.

Hãy nhớ rằng: Mặc dù ngoài kia có một số các thiết bị với công nghệ rất cao cấp và vẫn đang tiếp tục thúc đẩy quá trình phát triển, vẫn còn hầu hết trên thế giới là sử dụng loại thiết bị so với những quái vật thông số kỹ thuật đó không khác gì chiếc bàn tính với màn hình LCD.

Chúng tôi muốn giúp bạn khai thác chính xác sức mạnh của CSS3. Để làm điều đó chúng ta cần phải hiểu một vài những điều đầu tiên.

## *Hiểu về luồng hoạt động của trình duyệt*

Trình duyệt đang làm gì trong khi **render** các **Element**? Luồng hoạt động rất đơn giản này được gọi là ***Critical Rendering Path***.

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*wJKTvKHyYi13kPoI." src="https://cdn-images-1.medium.com/max/1600/0*wJKTvKHyYi13kPoI."></div>

Nguồn: www.csstriggers.com

Để đạt được những Animation mượt mà, chúng ta cần tập trung vào việc thay đổi các thuộc tính ảnh hưởng đến bước Tổng hợp, thay vì thêm áp lực này vào các **Layer** trước đó.

1. Styles

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*LDiyh_mOgH1n21wF." src="https://cdn-images-1.medium.com/max/1600/0*LDiyh_mOgH1n21wF."></div>

Trình duyệt bắt đầu tính toán các Style để áp dụng lên các **Element** - **Recalculate Style**.

2. Layout

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*X_6VTAJuRQCt1qXM." src="https://cdn-images-1.medium.com/max/1600/0*X_6VTAJuRQCt1qXM."></div>

Trong lớp kế tiếp, trình duyệt sẽ bắt đầu tạo ra hình dạng và vị trí cho từng **Element** đó - **Layout**. Đây là nơi trình duyệt đặt các thuộc tính cho trang như **width** và **height**, cũng **margins** của nó, hoặc **left**/ **top**/ **right**/ **bottom** cho đối tượng.

3. Paint

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*wJKTvKHyYi13kPoI." src="https://cdn-images-1.medium.com/max/1600/0*wJKTvKHyYi13kPoI."></div>

Trình duyệt bây giờ sẽ bắt đầu **fill** vào các pixel cho từng **Element** thành các **Layer**. Các thuộc tính mà nó sử dụng ví dụ như **box-shadow**, **border-radius**, **color**, **background-color** giữa các thuộc tính khác.

4. Composite

Đây là nơi bạn muốn thực hiện những **"magic"** của mình, vì đây là khi trình duyệt bắt đầu vẽ lên tất cả các **Layer** trên màn hình.

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*JHTvclhMvkYYEBEY." src="https://cdn-images-1.medium.com/max/1600/0*JHTvclhMvkYYEBEY."></div>

Các trình duyệt hiện đại có thể **"animate"** bốn **style** một cách rất tốt, sử dụng các thuộc tính **transform** và **opacity**.

* **Position  —  transform**: translateX(n) translateY(n) translateZ(n);
* **Scale  —  transform**: scale(n);
* **Rotation  —  transform**: rotate(ndeg);
* **Opacity  —  opacity**: n;

## *Làm thế nào để đạt đến điểm 60 khung hình trên giây (FPS)?*

Với suy nghĩ này, đã đến lúc bạn phải xắn tay áo lên và bắt tay vào việc.

Hãy bắt đầu với HTML. Chúng tôi sẽ tạo ra một cấu trúc rất đơn giản và đặt menu ứng dụng của chúng tôi trong một lớp **layout**.

```
<div class="layout">
    <div class="app-menu"></div>
    <div class="header">
        <div class="menu-icon"></div>
    </div>
</div>
```
<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*rXGvLKSlZGRmz4Jd." src="https://cdn-images-1.medium.com/max/1600/0*rXGvLKSlZGRmz4Jd."></div>

## *Hướng sai*

```
.app-menu {
    left: -300px;
    transition: left 300ms linear;
}

.app-menu-open .app-menu {
    left: 0px;
    transition: left 300ms linear;
}
```
Bạn đã thấy những thuộc tính mà chúng tôi thay đổi chứ? Ta nên tránh sử dụng  **transition** với các thuộc tính **left**/ **top**/ **right**/ **bottom**. Điều đó không tạo ra một Animation mượt bởi vì nó làm cho trình duyệt phải tạo lại **layout** mỗi lần thực thi, điều này sẽ ảnh hưởng đến tất cả **Element** của nó.

Kết quả là một thứ gì đó trông như thế này:

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*ZWyuzfeBSbFbQjOy." src="https://cdn-images-1.medium.com/max/1600/0*ZWyuzfeBSbFbQjOy."></div>

**Hoạt cảnh** đó không mượt mà chút nào. Chúng tôi đã kiểm tra với [DevTools Timeline](https://developers.google.com/web/tools/chrome-devtools/evaluate-performance/timeline-tool?hl=en) để xem những gì đang diễn ra bên trong và đây là kết quả:

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*y6jExBTCikGX2hVC." src="https://cdn-images-1.medium.com/max/1600/0*y6jExBTCikGX2hVC."></div>

***Phần màu xanh lá cây thể hiện thời gian render một Animation***

Điều này rõ ràng cho thấy FPS không đều và hiệu suất khá chậm.

Thanh màu xanh lá cây biểu thị FPS. Một thanh cao cho biết rằng hình ảnh động được hiển thị ở 60 FPS. Một thanh thấp biểu thị dưới 60 FPS. Vì vậy, lý tưởng nhất, bạn muốn thanh màu xanh lá cây luôn cao trên **Timeline**. Những thanh màu đỏ đó cũng biểu thị **jank**, vì vậy, thay vào đó, một cách khác để đánh giá sự tiến bộ của bạn là bằng cách loại bỏ những thanh màu đỏ đó.

## *Sử dụng **Transform***
```
.app-menu {
    -webkit-transform: translateX(-100%);
            transform: translateX(-100%);
    transition: transform 300ms linear;
}
.app-menu-open .app-menu {
    -webkit-transform: none;
            transform: none;
    transition: transform 300ms linear;
}
```
Các thuộc tính **transform** ảnh hưởng đến **Composite**. Ở đây, chúng tôi nói với trình duyệt rằng các **Layer** sẽ được vẽ và sẵn sàng hoạt động ngay khi thao tác bắt đầu, do đó sẽ có ít trục trặc hơn khi **render** **Animation**.

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*D9YAp9EQwbKunIZ-." src="https://cdn-images-1.medium.com/max/1600/0*D9YAp9EQwbKunIZ-."></div>

Đó chính xác là những gì **Timeline** cho thấy:

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*qc1qxqFudZPYpIUE." src="https://cdn-images-1.medium.com/max/1600/0*qc1qxqFudZPYpIUE."></div>

Kết quả đã bắt đầu tốt hơn, FPS đều đặn hơn và do đó, **Animation** mượt mà hơn.

## *Chạy Animation trên GPU*

Sau đó, hãy cùng đưa lên một tầm cao mới. Để thực sự làm cho nó chạy trơn tru và mượt mà, chúng tôi sẽ sử dụng GPU để **render** ra **Animation**.

```
.app-menu {
    -webkit-transform: translateX(-100%);
            transform: translateX(-100%);
    transition: transform 300ms linear;
    will-change: transform;
}
```

Mặc dù **translateZ()** hoặc **translate3d()** vẫn sẽ được một số trình duyệt sử dụng làm dự phòng, thuộc tính **will-change** chính là **"tương lai"**. Điều này làm là nó thúc đẩy các **Element** cho một **Layer** khác, vì vậy trình duyệt không phải xem xét **Layout** khi **render** hoặc **vẽ**.

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*ZeuG8kachde9iCnR." src="https://cdn-images-1.medium.com/max/1600/0*ZeuG8kachde9iCnR."></div>

Hãy cùng xem nó mịn như thế nào? **Timeline** đã chứng minh rằng:

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*ekofIUN-X7br1bIH." src="https://cdn-images-1.medium.com/max/1600/0*ekofIUN-X7br1bIH."></div>

FPS của **Animation** đã đều đặn hơn rất nhiều và **Animation** được hiển thị nhanh hơn nhiều ở đây. Nhưng vẫn còn một **Frame** dài chạy ở đó. Lúc đầu, vẫn còn một chút tắc nghẽn.

Nhớ lại cấu trúc HTML được tạo ngay từ đầu, hãy điều khiển div **app-menu** trên cấu trúc đó bằng cách sử dụng ***JavaScript***:

```
function toggleClassMenu() {
    var layout = document.querySelector(".layout");
    if(!layout.classList.contains("app-menu-open")) {
        layout.classList.add("app-menu-open");
    } else {
        layout.classList.remove("app-menu-open");
    }
}
var oppMenu = document.querySelector(".menu-icon");
oppMenu.addEventListener("click", toggleClassMenu, false);
```

Vấn đề ở đây là bằng cách thêm ***class*** đó trong div **layout**, chúng tôi đã làm cho trình duyệt tính toán lại các **style** một lần nữa - và điều đó ảnh hưởng đến hiệu suất **render**.

## *Giải pháp 60 FPS "Smooth as Butter"*

Thay vào đó, nếu chúng ta có ***menu*** được tạo bên ngoài **viewport** thì sao? Đặt nó ở trong một *"khu vực"* bị cô lập sẽ đảm bảo rằng bạn chỉ tác động đến **Element** mà bạn thực sự muốn **"animate"**.

Bởi vậy, chúng tôi đề xuất cấu trúc HTML như sau:

```
<div class="menu">
    <div class="app-menu"></div>
</div>
<div class="layout">
    <div class="header">
        <div class="menu-icon"></div>
    </div>
</div>
```

Và bây giờ chúng ta có thể kiểm soát trạng thái của **menu** theo một cách hơi khác. Chúng ta sẽ xử lý các **animation** trong một lớp bị loại bỏ khi thời gian chuyển đổi kết thúc, bằng cách sử dụng hàm **transitionend** trong ***JavaScript***.

```
function toggleClassMenu() {
    myMenu.classList.add("menu--animatable");	
    if(!myMenu.classList.contains("menu--visible")) {		
        myMenu.classList.add("menu--visible");
    } else {
        myMenu.classList.remove('menu--visible');		
    }	
}

function OnTransitionEnd() {
    myMenu.classList.remove("menu--animatable");
}

var myMenu = document.querySelector(".menu");
var oppMenu = document.querySelector(".menu-icon");
myMenu.addEventListener("transitionend", OnTransitionEnd, false);
oppMenu.addEventListener("click", toggleClassMenu, false);
myMenu.addEventListener("click", toggleClassMenu, false);
```

***Hãy đặt tất cả cùng với nhau và kiểm tra lại kết quả.***

Dưới đây là một ví dụ CSS3 được **"Style"** đầy đủ, với mọi thứ ở đúng vị trí của nó:

```
.menu {
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: hidden;
    pointer-events: none;
    z-index: 150;
}

.menu--visible {
    pointer-events: auto;
}

.app-menu {
    background-color: #fff;
    color: #fff;
    position: relative;
    max-width: 400px;
    width: 90%;
    height: 100%;
    box-shadow: 0 2px 6px rgba(0, 0, 0, 0.5);
    -webkit-transform: translateX(-103%);
            transform: translateX(-103%);
    display: flex;
    flex-direction: column;
    will-change: transform;
    z-index: 160;
    pointer-events: auto;            
}

.menu--visible .app-menu {
    -webkit-transform: none;
            transform: none;
}

.menu--animatable .app-menu {
    transition: all 130ms ease-in;
}

.menu--visible.menu--animatable  .app-menu {
    transition: all 330ms ease-out;
}

.menu:after {
    content: '';
    display: block;
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,0.4);
    opacity: 0;
    will-change: opacity;
    pointer-events: none;
    transition: opacity 0.3s cubic-bezier(0,0,0.3,1);
}

.menu--visible.menu:after {
    opacity: 1;
    pointer-events: auto;
}
```

Và **Timeline** cho chúng ta thấy điều gì?

<div style="display: flex; justify-content: center; padding: 20px"><img class="progressiveMedia-image js-progressiveMedia-image" data-src="https://cdn-images-1.medium.com/max/1600/0*mDp5_LD08xtZKQyS." src="https://cdn-images-1.medium.com/max/1600/0*mDp5_LD08xtZKQyS."></div>

***"Smooth as butter", right? :D***