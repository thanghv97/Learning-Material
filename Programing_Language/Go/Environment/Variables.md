# **Environment Variables**
  ||||
  |-|-|-|
  |[GOROOT](#goroot)|[GOPATH](#gopath)|[GOSUMDB](#gosumdb)|
  ||||

### `GOROOT`
  *GOROOT chỉ ra vị trí Go SDK được cài đặt trên máy. Chúng ta không cần thay đổi biến môi trường này, trừ trường hợp muốn sử dụng các phiên bản Go khác nhau*

### `GOPATH`

### `GOSUMDB`
  *Câu lệnh go sẽ xác thực mỗi module được tải về, kiểm tra mỗi bit tải về  phiên bản hôm nay có đúng với mỗi bit t tải về  phiên bản hôm qua không. Điều  này giúp phát hiện những thay đổi không mong muốn.*

  + [go.sum file](#go-sum-file)
  + [Add thêm private repository]

#### go.sum file
  Trong mỗi module, cùng với go.mod file, câu lệnh go cũng maintains go.sum file bao gồm mã checksum của những module phụ thuộc với những version đã được cache qua những lần get trước. Mỗi dòng trong go.sum file sẽ được format như sau:

  ```
    <module> <version>[/go.mod] <hash>
  ```

  

  