# **Deep Learning**
  + [Linear regression](#linear-regression)

## **Linear Regression**
  Thuật toán linear regression giải quyết các bài toán có đầu ra là giá trị thực, ví dụ: dự đoán giá nhà, dự đoán giá cổ phiếu, dự đoán tuổi,...

  + **Training**: Tìm đường thẳng (model) gần các điểm nhất
  + **Prediction**: Dự đoán dựa trên đường tìm được ở trên

### *Thiết lập công thức*
  + **Model**:
 ```
    phương trình đường thẳng: y = w1 * x + w0 // cần tìm w0, w1
 ```
  + **Loss Function**: sử dụng **MSE** (Mean Squared Error) để đánh giá sự chênh lệch
    $$
      \mathrm{J}=\frac{1}{2} * \frac{1}{n} \sum_{i=1}^n\left(\hat{y}_i-y_i\right)^2
    $$
    (n là số điểm dữ liệu)
    + J không âm
    + J càng nhỏ thì đường thẳng càng gần điểm dữ liệu. Nếu J = 0 thì đường thẳng đi qua tất cả các điểm dữ liệu.

### *Thuật toán Gradient Descent*
  là thuật toán tìm giá trị nhỏ nhất của hàm số f(x) dựa trên đạo hàm:
  1. Khởi tạo giá trị x = x0 tùy ý
  2. Gán x = x - learning_rate * f'(x)
  3. Tính lại f(x): Nếu f(x) đủ nhỏ thì dừng lại, ngược lại tiếp tục bước 2

  **Áp dụng vào bài toán**
  
  Ta cần tìm giá trị nhỏ nhất của hàm
  $$
    \mathrm{J}=\frac{1}{2} * \frac{1}{n} \sum_{i=1}^n\left(\hat{y}_i-y_i\right)^2 = \frac{1}{2} * \frac{1}{n} \sum_{i=1}^n\left(w_1 * x_i + w_0 - y_i\right)^2 
  $$
  + Áp dụng 
    $$ h(x) = f(g(x)) => h'(x) = f'(g) * g'(x) $$ 
    với 
    $$ f(x) = x^2 \quad \quad g(x) = (w_1 * x_i + w0 - y_i) $$
  + Ta có 

    + $\begin{aligned} \frac{df}{dw_0} = w_1 * x_i + w_0 - y_i \end{aligned}$

    + $\begin{aligned} \frac{df}{dw_1} = x_i * (w_1 * x_i + w_0 - y_i) \end{aligned}$
  + Do đó
    + $\begin{aligned} \frac{dJ}{dw_0} = \sum_{i=1}^nw_1 * x_i + w_0 - y_i \end{aligned}$
    + $\begin{aligned} \frac{dJ}{dw_1} = \sum_{i=1}^nx_i * (w_1 * x_i + w_0 - y_i) \end{aligned}$

  