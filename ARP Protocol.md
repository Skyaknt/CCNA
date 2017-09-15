# Giao thức ARP ( Address Resolution Protocol)
*Giao thức phân giải địa chỉ (Address Resolution Protocol hay ARP) là một giao thức truyền thông được sử dụng để chuyển địa chỉ từ tầng mạng (Internet layer) sang tầng liên kết dữ liệu theo mô hình OSI. Đây là một chức năng quan trọng trong giao thức IP của mạng máy tính. ARP được định nghĩa trong RFC 826 vào năm 1982, [1] là một tiêu chuẩn Internet STD 37.
ARP được sử dụng để từ một địa chỉ mạng (ví dụ một địa chỉ IPv4) tìm ra địa chỉ vật lý như một địa chỉ Ethernet (địa chỉ MAC), hay còn có thể nói là phân giải địa chỉ IP sang địa chỉ máy. ARP đã được thực hiện với nhiều kết hợp của công nghệ mạng và tầng liên kết dữ liệu, như IPv4, Chaosnet,..
Trong mạng máy tính của phiên bản IPv6, chức năng của ARP được cung cấp bởi Neighbor Discovery Protocol (NDP).*
## I. Chức năng

**Có 2 chức năng chính** :
  - Chuyển đổi địa chỉ IPv4 sang địa chỉ MAC
  - Duy trì bộ nhớ ánh xạ giữa IP vs MAC ( cache of mappings )
      - ARP cache : bộ nhớ của ARP chứa nội dung cặp địa chỉ MAC vs địa chỉ IP kèm theo.
## 1.	Chuyển đổi địa chỉ IP sang MAC :
-	Khi packets gửi từ tầng Network xuống Data links để đóng gói thành frames, có 1 cơ chế liên kết giữa địa chỉ IP ở tầng trên với địa chỉ MAC ở tầng dưới và lưu trong 1 bảng gọi là ARP table. 
    -	ARP table lưu trong Ram.
    -	Mỗi hàng trong ARP chứa 1 cặp : IP - MAC
-	Địa chỉ IP và địa chỉ MAC trong bảng gắn liền với nhau, từ địa chỉ IP có thể truy ra địa chỉ MAC của thiết bị.
-	Sử dụng trong mạng LAN nội bộ
-	**Hoạt động** : một host A muốn gửi dữ liệu tới host B, nhưng chỉ biết địa chỉ IP của B , nó kiểm tra trong bảng ánh xạ ARP xem có cặp địa chỉ IP – MAC nào của B không, có thì n sẽ căn cứ vào địa chỉ MAC đó và gửi tới địch.
o	Trường hợp không có, host A sẽ gửi 1 bản tin ARP request đến các host kèm theo địa chỉ IP của máy B, khi máy B nhận được, nó sẽ kiểm tra , nếu đúng địa chỉ IP của nó , máy B sẽ gửi bản tin trả lời lại kèm theo địa chỉ MAC của mình. Máy A căn cứ vào đó gửi bản tin tới máy B.
## 2.	Duy trì bộ nhớ ánh xạ ARP :

Có 2 cách để thu thập địa chỉ IP -MAC :

-	Kiểm soát đường truyền trong phân vùng mạng :  Một node nhận các frames đi qua, nó sẽ lưu lại địa chỉ IP và MAC của các Frame đó rồi ánh xạ chúng thành các cặp.

-	Thiết bị gửi 1 bản tin broadcast gọi là bản tin ARP request đến tất cả các host trong mạng LAN. Frame đó chứa IP của máy đích. Máy nào nhận được kiểm tra đúng là IP máy mình thì gửi lại một bản tin ARP reply bao gồm địa chỉ MAC của nó. Máy gửi nhận được và lưu cặp IP-MAC đó vào ARP table.

    - Nếu trường hợp không có thiết bị nào phản hồi lại, packet sẽ bị xóa. Việc gửi bị thất bại này sẽ được báo lên các tầng trên, ở một số thiết bị  như router , nó sẽ quyết định có nên gửi đến máy nguồn 1 bản tin ICMPv4 thông báo lỗi hay không.
-	Các cặp ánh xạ này sẽ được lưu trong một thời gian nhất định, sau một thời gian không có sự giao tiếp địa chỉ này sẽ bị xóa.
 
## II. Cơ chế định tuyến của ARP : 

### 1. ARP với máy đích nằm ngoài mạng local :

Khi một host A muốn gửi tới host B nhưng B nằm ngoài vùng mạng LAN của nó.
-	Host A không có địa chỉ MAC của máy nguồn , nó sẽ gửi bản tin ARP request tới thiết bị Router ( hoặc next hop ) bằng đường gateway để xác định MAC của router. 
-	Router gửi bản tin phản hồi lại kèm theo địa chỉ MAC của nó cho host A.
-	Host A lưu vào bảng ARP cặp IP-MAC của router, và tiến hành gửi tin .
-	Router nhận được gói tin, căn cứ vào địa chỉ IP đích và port đã lưu trong bảng routing table , router gửi bản tin ARP request để tìm địa chỉ MAC của máy B .
-	Máy B nhận được bản tin request, reply lại bao gồm địa chỉ MAC của mình, router sẽ gửi bản tin từ máy A đến máy B.

### 2.Sử dụng Proxy ARP : 

