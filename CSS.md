# CSS Flexbox Layout Module: DÀN TRANG VỚI CSS FLEXBOX TOÀN TẬP
Trong CSS, từ trước tới nay nếu chúng ta muốn dàn layout của trang thì sẽ sử dụng các thuộc tính float và kỹ thuật clear float để chia cột website như ý muốn. Hoặc muốn thuận tiện hơn thì sử dụng các CSS Grid Framework để tiết kiệm thời gian. Nhưng nói thật, nếu bạn đã từng làm việc với CSS thường xuyên thì việc chia cột đôi khi rất tốn thời gian với kỹ thuật truyền thống này, còn dùng framework thì lại khiến website chúng ta có thêm nhiều đoạn CSS không cần thiết. Hoặc là nếu chúng ta dàn trang trên kỹ thuật thông thường hiện nay thì ở mỗi thiết bị khác nhau mình phải cân đối lại kích thước khá phức tạp.

CSS3 ra đời giống như phiên bản cải thiện những nhược điểm hiện có của nó, trong đó bao gồm luôn việc cải thiện kỹ thuật dàn trang linh hoạt hơn, đơn giản hơn và thuộc tính CSS3 chúng ta sử dụng để dàn trang là Flexbox.

# Flexbox là gì?
Flexbox là một kiểu dàn trang (layout mode) mà nó sẽ tự cân đối kích thước của các phần tử bên trong để hiển thị trên mọi thiết bị. Nói theo cách khác, bạn không cần thiết lập kích thước của phần tử, không cần cho nó float, chỉ cần thiết lập nó hiển thị chiều ngang hay chiều dọc, lúc đó các phần tử bên trong có thể hiển thị theo ý muốn.

Hiện nay, theo lời khuyên từ Mozilla thì chúng ta sử dụng Flexbox để thiết lập bố cục trong phạm vi nhỏ (ví dụ như những khung trong website) và khi thiết lập bố cục ở phạm vi lớn hơn (như chia cột website) thì vẫn nên sử dụng kiểu thông thường là dàn trang theo dạng lưới (grid layout).

# Thuật ngữ các thành phần trong Flexbox
Trước khi đi vào tìm hiểu sâu hơn về Flexbox, chúng ta cần nắm qua cấu trúc của Flexbox là như thế nào và một số thuật ngữ liên quan.

Dưới đây là sơ đồ cấu trúc Flexbox từ Mozilla Developer Network.

flex_termsNguồn: Mozilla Developer Network
Hai thành phần quan trọng nhất trong một bố cục Flexbox là gồm container và item:

container: là thành phần lớn bao quanh các phần tử bên trong, bạn sẽ thiết lập kiểu hiển thị inline (sắp xếp theo chiều ngang) hoặc kiểu sắp xếp theo chiều dọc. Khi đó, các item bên trong sẽ hiển thị dựa trên thiết lập của container này.
item: Các phần tử con của container được gọi là item, ở item bạn có thể thiết lập nó sẽ sử dụng bao nhiêu cột trong một container, hoặc thiết lập thứ tự hiển thị của nó.
Ngoài hai thành phần chính đó, chúng ta có thể thấy hình trên sẽ có:

main start, main end: Khi thiết lập flexbox, điểm bắt đầu của container gọi là main start và điểm kết thúc được gọi là main end. Điều này có nghĩa, các item bên trong sẽ heienr thị từ main start đến main end (hoặc là được phép hiển thị đến main end). Và chiều vuông góc của nó là cross start, cross end cũng có ý nghĩa tương tự nhưng luôn vuông góc với main start, main end.
main axis: Trục này là trục chính để điều khiển hướng mà các item sẽ hiển thị. Như bạn thấy ở trên hình main axis là trục dọc nên các item sẽ hiển thị theo chiều dọc, tuy nhiên ta có thể sử dụng thuộc tính flex-direction để thay đổi trục của main axis và lúc đó các item sẽ hiển thị theo nó. Và cross axis luôn là trục vuông góc của main axis.
main size: Bạn có thể hiểu đơn giản là kích thước (chiều rộng hoặc dọc) của mỗi item dựa theo trục main axis.
cross size: Là kích thước (chiều rộng hoặc dọc) của mỗi item dựa theo trục cross axis.
Bắt đầu với Flexbox
Trước tiên mình bắt đầu với một cấu trúc đơn giản sau:
</p>
<p>&lt;div class=&quot;container&quot;&gt;</p>
<p>   &lt;div class=&quot;item item1&quot;&gt;1&lt;/div&gt;</p>
<p>   &lt;div class=&quot;item item2&quot;&gt;2&lt;/div&gt;</p>
<p>   &lt;div class=&quot;item item3&quot;&gt;3&lt;/div&gt;</p>
<p>   &lt;div class=&quot;item item4&quot;&gt;4&lt;/div&gt;</p>
<p>&lt;/div&gt;</p>
<p>
Và một đoạn CSS ban đầu để thiết lập màu sắc và kích thước để dễ nhìn từng thành phần:
<br />
/** Global CSS **/<br />
.container {<br />
 background: red;<br />
 max-width: 960px;<br />
 max-height: 1000px;<br />
 margin: 0 auto;<br />
 padding: 5px;<br />
}<br />
.item {<br />
 background: blue;<br />
 margin: 5px;<br />
 color: white;<br />
 height: 50px;<br />
 text-align: center;<br />
 line-height: 50px;<br />
}<br />
Bây giờ chúng ta sẽ bắt đầu làm việc với Flexbox ở đây. Trước tiên chúng ta sẽ đưa .container về hiển thị ở dạng flexbox với display: flex.
<br />
/** Flex layout **/<br />
.container {<br />
 display: flex;<br />
}<br />
Bạn sẽ thấy các item bên trong đã tự hiển thị theo chiều dọc, tương ứng với trục main axis mặc định là chiều ngang.

css-flexbox-01

Nếu bạn muốn đổi trục thì chỉ cần thêm thuộc tính flex-direction vào container. Cụ thể:

01
flex-direction: row | column | row-reverse | column-reverse
flex-direction:
row: Chuyển trục main axis thành chiều ngang, nghĩa là hiển thị theo hàng.
colum: Chuyển trục main axis thành chiều dọc, nghĩa là hiển thị theo cột.
row-reverse: Hiển thị theo hàng nhưng đảo ngược vị trí các item.
column-reverse: Hiển thị theo cột nhưng đảo ngược vị trí các item.
css-flexbox-02

Quá đơn giản đúng không?

flex-wrap
Bây giờ để hiểu cái này, chúng ta thử thêm chiều rộng cho mỗi item bên trong là 1000px xem chuyện gì sẽ xảy ra khi dùng flexbox.
<br />
.item {<br />
 width: 1000px;<br />
}<br />
css-flexbox-03

Như bạn thấy, dù chúng ta có thêm chiều rộng cho mỗi item bên trong là 1000px nhưng nó vẫn hiển thị trên một hàng đều nhau. Lý do là mặc định, flexbox tự căn chỉnh các phần tử hiển thị đều nhau theo trục main axis của nó dựa theo chiều rộng của container. Vì vậy cho dù bạn có chỉnh chiều rộng vượt quá giới hạn của nó thì nó vẫn không bị nhảy lung tung.

Bây giờ hãy thử thêm thuộc tính flex-wrap: wrap vào container thử nhé.
.container {<br />
 display: flex;<br />
 flex-wrap: wrap;<br />
}
css-flexbox-04

Nói nôm na là thuộc tính này cho phép container có thể bọc lại các item kể cả khi kích thước của item bị thay đổi, mặc định là nowrap. Thuộc tính này có thể áp dụng với cả chiều dọc của container và item. Các bạn xem video ở trên để rõ hơn.

order
Trong đoạn HTML ví dụ của mình trong bài này, mình có đặt số thứ tự cho mỗi phần tử là 1, 2, 3 và 4 với class tương ứng là .item1, .item, .item3 và .item4. Mặc định item này sẽ hiển thị theo thứ tự trong HTML, nhưng với thuộc tính order chúng ta có thể sắp xếp lại vị trí sắp xếp của các item.

Ví dụ mình có:
<br />
.item1 {<br />
 order: 4;<br />
}<br />
.item2 {<br />
 order: 3;<br />
}<br />
.item3 {<br />
 order: 1;<br />
}<br />
.item4 {<br />
 order: 2;<br />
}<br />
css-flexbox-05

Mặc định thứ tự sắp xếp sẽ bắt đầu từ bên trái qua phải, từ trên xuống dưới. Nếu bạn chỉnh lại trục của main axis với thuộc tính flex-direction nó sẽ thay đổi ngược lại.

flex-grow
Để làm ví dụ này trước tiên mình hãy bỏ chức năng wrap đi và thiết lập chiều rộng của item là 50px.
<br />
.item {<br />
 width: 50px;<br />
}<br />
Bây giờ ở .item2, mình cho giá trị flex-grow là 1 thử nhé.
.item2 {<br />
 flex-grow: 1;<br />
}
css-flexbox-06

Khi thiết lập nó flex-grow là 1, thì nó sẽ lấy phần trống còn lại của container đắp vào. Bây giờ hãy thử cho .item1 với flex-grow: 2 thử.
<br />
.item1 {<br />
 flex-grow: 2;<br />
}<br />
css-flexbox-07edited

Lúc này giá trị flex-grow: 2 sẽ lấy phần dư lớn gấp đôi của flex-grow: 1.

flex-shrink
Bạn có thể hiểu mặc định tất cả các item đều có giá trị flex-shrink là 1. Điều này có nghĩa là khi chúng ta thu nhỏ trình duyệt lại, các phần tử đều co lại bằng nhau. Tuy nhiên giả sử mình muốn .item3 nó co lại nhiều hơn so với các item khác thì mình sẽ tăng giá trị flex-shrink của nó lên.
<br />
.item3 {<br />
 flex-shrink: 2;<br />
}<br />
css-flexbox-08

flex-basis
Cái này bạn có thể hiểu đơn giản nhất là gán cho item một kích thước nhất định. Bạn có thể sử dụng giá trị tuyệt đối hoặc tương đối (căn cứ theo kích thước của container).
<br />
.item3 {<br />
 flex-basis: 500px;<br />
}<br />
css-flexbox-09

# justify-content
Mặc định các item bên trong sẽ rải đều bắt đầu từ main start đến main end, tuy nhiên nếu container vẫn còn khoảng trống thì có thể dùng thuộc tính justify-content để điều chỉnh lại vị trí bắt đầu của nó.

Thuộc tính này có 5 giá trị và bạn có thể xem tấm ảnh bên dưới mình mượn của CSS Tricks để hiểu hơn về ý nghĩa các giá trị của justify-content.

flexbox-justify-content

# Đây là ví dụ:
<br />
.container {<br />
 display: flex;<br />
 justify-content: flex-end;<br />
}<br />
css-flexbox-10

Trong bài này mình chỉ đề cập tới một số thuộc tính hay dùng trong Flexbox thôi, bạn có thể xem thêm danh sách thuộc tính Flexbox tại đây.

# Lời kết
Flexbox trong CSS có thể nói là một trong những kiểu dàn trang rất tốt để thay thế cho cách dàn trang thông thường là dùng float, thích hợp khi dàn trang những thành phần nhỏ trong website để hạn chế tối đa việc dùng float không cần thiết.

Mặc dù hiện tại chưa phải tất cả trình duyệt đều hỗ trợ CSS Flexbox nhưng trong tương lai, chắc chắn đây là một trong những tính năng mà các trình duyệt sẽ sớm hỗ trợ do khả năng tiện dụng và tùy biến tốt của nó mang lại.
