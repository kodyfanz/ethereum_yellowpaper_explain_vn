# Bảng ký hiệu
## Quy ước chung
|Thành phần                 |Quy ước                        |Ví dụ
|------                     |------                         |------
|Cấu trúc bậc cao           |Chữ Hy Lạp viết thường đậm     |$\mathbf{\sigma}$: trạng thái thế giới;<br>$\mathbf{\mu}$: trạng thái máy  
|Hàm trên cấu trúc bậc cao  |Chữ Hy Lạp viết hoa            |$\mathbf{\Upsilon}$, hàm chuyển đổi trạng thái Ethereum
|Hàm thông thường khác      |Chữ viết hoa, có thể có ghi chú phụ ở dưới |$C$: hàm chi phí chung;<br>$C_{SSTORE}$: hàm chi phí cho việc thưc thi opcode SSTORE
|Hàm đặc biệt               |Nhiều ký tự                    |$\texttt{KEC}$: hàm băm Keccak-256;<br>$\texttt{KEC512}$: hàm băm Keccak-512
|Bộ dữ liệu (tuple)         |Chữ viết hoa                   |$T$: một giao dịch
|Thành phần của bộ dữ liệu  |Ghi chú phụ ở dưới (nếu viết hoa nghĩa là đại diện cho một bộ dữ liệu)   |$T_n$: nonce của giao dịch;<br>$I_H$: header của khối hiện tại
|Giá trị vô hướng, dãy bytes có độ dài cố định/ mảng        |Chữ viết thường, thỉnh thoảng dùng chữ Hy Lạp  |$n$: nonce của giao dịch;<br>$\delta$: số lượng mục trong ngăn xếp được yêu cầu
|Dãy có độ dài bất kỳ       |Chữ thường viết đậm            |$\boldsymbol{o}$: dữ liệu đầu ra của message-call
|Tập hợp                    |Chữ 2 nét viết hoa             |$\mathbb{P}_{256}$: số nguyên dương nhỏ hơn $2^{256}$;<br>$\mathbb{B}\_{32}$: dãy 32 bytes
|Thành phần hoặc dãy phụ của một dãy  |Dấu ngoặc vuông  |$\mathbf{{\mu}_s}[0]$: phần tử đầu tiên trong ngăn xếp;<br>$\mathbf{{\mu}_m}[0..31]$: 32 phần tử đầu tiên trong memory
|Giá trị mới sau phép biến đổi  |Dấu phẩy ở trên  |$g'$: gas còn lại
|Giá trị trung gian | Dấu sao ở trên  |$g^*$: gas hoàn lại;<br>$g^{**}$: gas còn lại sau khi thực thi code
|Phép biến đổi theo phần tử |Dấu phẩy ở trên hàm  |$f^*\big((x_0, x_1, ...) \big) \equiv \big(f(x_0), f(x_1), ... \big)$: cho mọi hàm $f$

## Ký hiệu cụ thể
### Ký hiêụ trên các cấu trúc bậc cao
|Ký hiệu            |Mô tả
|------             |------
|$\mathbf{\sigma}$    |Trạng thái thế giới (world-state), bao gồm tất cả trạng thái của tất cả tài khoản gồm luôn thành phần con của nó như: nonce, balances, storage, và code
|$\mathbf{\sigma}_t$  |Trạng thái thế giới tại thời điểm $t$
|$\mathbf{\mu}$       |Bộ dữ liệu (tuple) của Trạng thái máy, $(g, pc, m, i, s)$: gas, program counter, memory, memory size, stack
|$T$                |Một giao dịch (transation) Ethereum
|$T_0, T_1, ...$    |Các giao dịch trong một khối (block)
|$B$                |Một khối (block): $B \equiv \big(..., (T_0, T_1, ...), ...\big)$ - nghĩa là khối $B$ gồm nhiều giao dịch bên trong cùng với các thành phần khác xung quanh
|$\Upsilon$         |Hàm chuyển đổi trạng thái Ethereum: $\sigma_{t+1} \equiv \Upsilon(\mathbf{\sigma_{t}}, T)$ - nghĩa là trạng thái ở thời điểm $t+1$ là kết quả của phép biến đổi $\Upsilon$ trên số liệu đầu vào là trạng thái ở thời điểm $t$ trước đó $\sigma_{t}$ và tác nhân giao dịch $T$ gây ra
|$\Pi$              |Hàm chuyển đổi trạng thái cấp khối: $\Pi(\mathbf{\sigma}, B) \equiv \Upsilon\big(\Upsilon(\mathbf{\sigma}, T_0), T_1)...\big)$ - ở đây ta thấy $\Upsilon\big(\Upsilon(\mathbf{\sigma}, T_0), T_1)...\big)$ là một hàm đệ quy, thực hiện lượt qua tất cả các giao dịch $T_i$ có trong khối $B$, cuối cùng trả về trạng thái thế giớ ở khối $B$ sau khi hoàn thiện

### Trạng thái thế giới (World state)
|Ký hiệu            |Mô tả
|------             |------
|$\sigma[a]$        |Trạng thái của tài khoản $a$, là một bộ (tuple) gồm (none, balance, storageRoot, codeHash)
|$\sigma[a]_n$      |Nonce của tài khoản $a$
|$\sigma[a]_b$      |Số dư của tài khoản $a$
|$\sigma[a]_s$      |Một hash 256-bit của nút gốc (root node) của cây Merkle Patricia mã hóa nội dung của các dữ liệu tài khoản $a$.
|$\sigma[a]_c$      |Một hash 256-bit của EVM-code của tài khoản $a$, bằng $\texttt{KEC}(\boldsymbol{b})$ trong đó $\boldsymbol{b}$ là code của tài khoản $a$

Chú ý rằng 
```math
\texttt{TRIE}\big(L^*_I( \sigma [a]_\boldsymbol{s} )\big) \equiv \sigma[a]_s 
```
Trong đó $L^*_I$ là phép biến đổi theo phần tử 
```math
L_I\big((k,v)\big)\equiv\big((\texttt{KEC}(k),\texttt{RLP}(v))\big)
```
Chữ $\boldsymbol{s}$ trong $L_I(\sigma[a]_{\boldsymbol{s}})$ được viết đậm hàm ý rằng phép biến đổi thao tác trên bộ (tuple) dữ liệu trạng thái thật trong storage của tài khoản $a$ chứ không phải là hash của nó. Như vậy $L^*_I$ thao tác lượt qua tất cả giá trị được lưu trong storage của tài khoản $a$ và trả về là một bộ (tuple) làm tham số cho hàm $\texttt{TRIE}$, hàm $\texttt{TRIE}$ sẽ thao tác trên bộ (tuple) này và trả về hash 256-bit chính là storageRoot của tài khoản $a$
