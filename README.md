# Tìm hiểu Ethereum Yellow Paper phiên bản Paris
Làm rõ những điểm khó hiểu trong Giấy vàng Ethereum

## Lý do
Mặt dù đã có bản dịch tiếng Việt đầy đủ của Giấy vàng Ethereum, nhưng bản dịch đã cố gắng dịch sát nghĩa những từ ngữ dùng trong bối cảnh của tài liệu đó, nên không tránh khỏi những sự khó hiểu cho đa số đọc giả. Tài liệu này nhằm mục đích giải thích cho những khúc mắt nếu có đó. 
Tài liệu sẽ liên tục cập nhật cũng như có thể bổ sung thêm kiến thức liên quan giúp cho quá trình tìm hiểu Giấy vàng Ethereum được thuận tiện.

## Một số quy ước
Một số loại đối tượng tên gọi khác nhau nhưng có cách hiểu dễ gây nhầm lẫn hoặc gần giống nhau, để thống nhất mỗi khi đọc từ tiếng Việt chúng ta liên tưởng chỉ mỗi một từ tiếng Anh duy nhất, chúng ta quy ước cách dịch:

| Tiếng Anh | Tiếng Việt | Đặt điểm |
| --------- | ---------- | --------- |
| array     | mảng       | Các phần tử cùng loại dữ liệu, có thể truy xuất được thông qua chỉ mục |
| list      | danh sách  | Các phần tử có thể thay đổi (thêm, sửa, xóa), có thể truy xuất được thông qua chỉ mục |
| tuple     | bộ         | Các phần tử có thể khác loại dữ liệu, không thể thay đổi, có thể truy xuất được thông qua chỉ mục |
| set       | tập hợp    | Một nhóm các phần tử không có thứ tự và không có các phần tử trùng lặp |
| string    | chuỗi      | Gồm nhiều ký tự liên tiếp nhau, tùy thuộc vào bảng mã mà mỗi ký tự có độ dài byte khác nhau |
| sequence | dãy        | Các phần tử có thứ tự và có thể truy xuất thông qua chỉ mục. Bao gồm chuỗi, danh sách, và bộ |
|series     | loạt       | Loạt dữ liệu, không quan trọng các vấn đề loại, thứ tự, khả năng thay đổi, truy xuất |

## Nội dung (cập nhật liên tục)
[Bảng ký hiệu](docs/conventions)

## Giấy phép
Được cấp phép theo [Giấy phép MIT](./LICENSE)
