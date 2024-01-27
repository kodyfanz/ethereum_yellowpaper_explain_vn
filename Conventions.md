# Bảng ký hiệu
## Quy ước chung
|Thành phần                 |Quy ước                        |Ví dụ                                        |
|---------------------------|-------------------------------|---------------------------------------------|
|Cấu trúc bậc cao           |Chữ Hy Lạp viết thường đậm     |$\mathbf{\sigma}$: trạng thái thế giới;<br>$\mathbf{\mu}$: trạng thái máy  |
|Hàm trên cấu trúc bậc cao  |Chữ Hy Lạp viết hoa            |$\Upsilon$, hàm chuyển đổi trạng thái Ethereum |
|Hàm thông thường khác      |Chữ viết hoa, có thể có ghi chú phụ ở dưới |$C$: hàm chi phí chung;<br>$C_\texttt{SSTORE}$: hàm chi phí cho việc thưc thi opcode $\texttt{SSTORE}$ |
|Hàm đặc biệt               |Nhiều ký tự                    |$\texttt{KEC}$: hàm băm Keccak-256;<br>$\texttt{KEC512}$: hàm băm Keccak-512 |
|Bộ dữ liệu (tuple)         |Chữ viết hoa                   |$T$: một giao dịch |
|Thành phần của bộ dữ liệu  |Ghi chú phụ ở dưới (nếu viết hoa nghĩa là đại diện cho một bộ dữ liệu (tuple))   |$T_n$: nonce của giao dịch;<br>$I_H$: header của khối hiện tại (là 1 bộ (tuple)) |
|Giá trị vô hướng, dãy bytes có độ dài cố định/ mảng        |Chữ viết thường, thỉnh thoảng dùng chữ Hy Lạp  |$n$: nonce của giao dịch;<br>$\delta$: số lượng mục trong ngăn xếp được yêu cầu |
|Dãy có độ dài bất kỳ       |Chữ thường viết đậm            |$\boldsymbol{o}$: dữ liệu đầu ra của message-call |
|Tập hợp                    |Chữ 2 nét viết hoa             |$\mathbb{P}_{256}$: số nguyên dương nhỏ hơn $2^{256}$; <br>$\mathbb{B}\_{32}$: dãy 32 bytes |
|Thành phần hoặc dãy phụ của một dãy  |Dấu ngoặc vuông  |$\mathbf{\mu_s}[0]$: phần tử đầu tiên trong ngăn xếp;<br>$\mathbf{\mu_m}[0..31]$: 32 phần tử đầu tiên trong memory |
|Giá trị mới sau phép biến đổi  |Dấu phẩy ở trên  |$g'$: gas còn lại |
|Giá trị trung gian | Dấu sao ở trên  |$g^*$: gas hoàn lại;<br>$g^{**}$: gas còn lại sau khi thực thi code |
|Phép biến đổi theo phần tử |Dấu phẩy ở trên hàm  |$f^*\big((x_0, x_1, ...) \big) \equiv \big(f(x_0), f(x_1), ... \big)$: cho mọi hàm $f$ |

## Ký hiệu cụ thể
### Ký hiêụ trên các cấu trúc bậc cao
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
|$\mathbf{\sigma}$    |Trạng thái thế giới (world-state), bao gồm tất cả trạng thái của tất cả tài khoản gồm luôn thành phần con của nó như: nonce, balances, storage, và code |
|$\mathbf{\sigma}_t$  |Trạng thái thế giới tại thời điểm $t$ |
|$\mathbf{\mu}$       |Bộ dữ liệu (tuple) của Trạng thái máy, $(g, pc, m, i, s)$: gas, program counter, memory, memory size, stack |
|$T$                |Một giao dịch (transation) Ethereum |
|$T_0, T_1, ...$    |Các giao dịch trong một khối (block) |
|$B$                |Một khối (block): $B \equiv \big(..., (T_0, T_1, ...), ...\big)$ - nghĩa là khối $B$ gồm nhiều giao dịch bên trong cùng với các thành phần khác xung quanh |
|$\Upsilon$         |Hàm chuyển đổi trạng thái Ethereum: $\sigma_{t+1} \equiv \Upsilon(\mathbf{\sigma_{t}}, T)$ - nghĩa là trạng thái ở thời điểm $t+1$ là kết quả của phép biến đổi $\Upsilon$ trên số liệu đầu vào là trạng thái ở thời điểm $t$ trước đó $\sigma_{t}$ và tác nhân giao dịch $T$ gây ra |
|$\Pi$              |Hàm chuyển đổi trạng thái cấp khối: $\Pi(\mathbf{\sigma}, B) \equiv \Upsilon\big(\Upsilon(\mathbf{\sigma}, T_0), T_1)...\big)$ - ở đây ta thấy $\Upsilon\big(\Upsilon(\mathbf{\sigma}, T_0), T_1)...\big)$ là một hàm đệ quy, thực hiện lượt qua tất cả các giao dịch $T_i$ có trong khối $B$, cuối cùng trả về trạng thái thế giớ ở khối $B$ sau khi hoàn thiện |

### Trạng thái thế giới (World state)
| Ký hiệu                    | Mô tả                                     |
| -------------------------- | ----------------------------------------- |
|$\mathbf{\sigma}[a]$        |Trạng thái của tài khoản $a$, là một bộ (tuple) gồm (none, balance, storageRoot, codeHash): $\mathbf{\sigma}[a] \equiv (\mathbf{\sigma}[a]_n, \mathbf{\sigma}[a]_b, \mathbf{\sigma}[a]_s, \mathbf{\sigma}[a]_c)$ |
|$\mathbf{\sigma}[a]_n$      |Nonce của tài khoản $a$ |
|$\mathbf{\sigma}[a]_b$      |Số dư của tài khoản $a$ |
|$\mathbf{\sigma}[a]_s$      |Một hash 256-bit của nút gốc (root node) của cây Merkle Patricia mã hóa nội dung của các dữ liệu tài khoản $a$. |
|$\mathbf{\sigma}[a]_c$      |Một hash 256-bit của EVM-code của tài khoản $a$, bằng $\texttt{KEC}(\boldsymbol{b})$ trong đó $\boldsymbol{b}$ là code của tài khoản $a$ |

Chú ý rằng 
```math
\texttt{TRIE}\big(L^*_I( \sigma [a]_\boldsymbol{s} )\big) \equiv \sigma[a]_s 
```
Trong đó $L^*_I$ là phép biến đổi theo phần tử 
```math
L_I\big((k,v)\big)\equiv\big((\texttt{KEC}(k),\texttt{RLP}(v))\big)
```
Chữ $\boldsymbol{s}$ trong $L_I(\sigma[a]_{\boldsymbol{s}})$ được viết đậm hàm ý rằng phép biến đổi thao tác trên bộ (tuple) dữ liệu trạng thái thật trong storage của tài khoản $a$ chứ không phải là hash của nó. Như vậy $L^*_I$ thao tác lượt qua tất cả giá trị được lưu trong storage của tài khoản $a$ và trả về là một bộ (tuple) làm tham số cho hàm $\texttt{TRIE}$, hàm $\texttt{TRIE}$ sẽ thao tác trên bộ (tuple) này và trả về hash 256-bit chính là storageRoot của tài khoản $a$

### Trạng thái máy (Machine state)
| Ký hiệu                    | Mô tả                                     |
| -------------------------- | ----------------------------------------- |
|$\mathbf{\mu}_g$            |Lượng gas hiện có |
|$\mathbf{\mu}_{pc}$         |Bộ đếm chương trình (program counter) |
|$\mathbf{\mu}_\mathbf{m}$   |Nội dung bộ nhớ (memory) |
|$\mathbf{\mu}_i$            |Số lượng từ (words) trong bộ nhớ |
|$\mathbf{\mu}_\mathbf{s}$   |Ngăn xếp (stack) |
|$\mathbf{\mu}_\mathbf{s}[n]$         |Mục thứ $n$ trong ngăn xếp (mục ở độ sâu $n$) |

### Trạng thái con (Substate)
| Ký hiệu           | Mô tả                                     |
| ----------------- | ----------------------------------------- |
|$A$                |Một trạng thái con trong quá trình thực thi, là một bộ (tuple): $A \equiv (A_\mathbf{s}, A_\mathbf{l}, A_\mathbf{t}, A_r, A_\mathbf{a}, A_\mathbf{K})$ |
|$A_\mathbf{s}$     |Tập hợp tự hủy (self-destruct), là tập hợp các account sẽ bị loại bỏ khi giao dịch hoàn tất. |
|$A_\mathbf{l}$     |Một loạt các nhật ký (log series) |
|$A_\mathbf{t}$     |Tập hợp các account đã chạm vào, trong đó các tài khoản trống sẽ bị xóa vào cuối giao dịch |
|$A_r$              |Số dư gas để hoàn lại |
|$A_\mathbf{a}$     |Tập hợp các tài khoản đã truy cập |
|$A_\mathbf{K}$     |Tập hợp các storage key đã truy cập, mỗi phần tử của $A_\mathbf{K}$ là một bộ (tuple) của 20-byte địa chỉ tài khoản và 32-byte khe lưu trữ (storage slot)
|$A^0$              |Trạng thái con rỗng: $A^0 \equiv \big(\varnothing, (), \varnothing, 0, \pi, \varnothing\big)$, trong đó $\pi$ là tập hợp của tất cả các địa chỉ hợp đồng được biên dịch trước |

### Môi trường thực thi (Execution enviroment)
| Ký hiệu           | Mô tả                                     |
| ----------------- | ----------------------------------------- |
|$I$                |Bộ (tuple) các phần tử sau đây được cung cấp cho môi trường thực thi |
|$I_a$              |Địa chỉ của tài khoản sở hữu code thực thi (địa chỉ hợp đồng) |
|$I_o$              |Địa chỉ của người gửi giao dịch (sender) |
|$I_p$              |Giá của gas trong giao dịch |
|$I_\mathbf{d}$     |Mảng byte, là dữ liệu đầu vào của quá trình thực thi; nếu tác nhân thực thi là một giao dịch thì đây là dữ liệu giao dịch |
|$I_s$              |Địa chỉ của account đã làm cho việc thực thi xảy ra; nếu tác nhân thực thi là một giao dịch thì đây là người gửi giao dịch (sender) |
|$I_v$              |Giá trị (value) tính bằng Wei truyền vào tài khoản; nếu tác nhân thực thi là một giao dịch thì đây là giá trị giao dịch |
|$I_\mathbf{b}$     |Mảng byte, là mã máy (machine code) để thực thi |
|$I_H$              |Header của khối hiện tại |
|$I_e$              |Độ sâu của message-call hoặc tạo hợp đồng (tức là số lượng CALL hoặc CREATE2 đang được thực thi ở thời điểm hiện tại). Việc xác định độ sâu này nhằm mục đích ngăn chặn gọi đệ quy vô hạn và kiểm soát tiêu tốn gas |
|$I_w$              |Cờ cho quyền sửa đổi trạng thái. Xem EIP-214, STATICCALL |

### Thực thi (Execution)
| Ký hiệu           | Mô tả                                     |
| ----------------- | ----------------------------------------- |
|$\Xi$              |Hàm thực thi code $(\boldsymbol{\sigma}', g', A', \mathbf{o}) \equiv \Xi(\boldsymbol{\sigma}, g, A, I)$ |
|$\mathbf{o}$       |Dữ liệu đầu ra của message-call, $\mathbf{o} \equiv H(\boldsymbol{\mu}, I)$. Khi tạo hợp đồng, mã byte hợp đồng sẽ được triển khai. |
|$\mathbf{i}$       |Mã EVM khởi tạo cho hợp đồng mới được triển khai (constructor) |
|$H(\mathbf{\mu}, I)$ |Hàm tạm dừng bình thường, thường là giá trị được cung cấp bởi sự trở lại hoặc hoàn nguyên opcode hoặc trống trong trường hợp dừng. |
|$Z(\mathbf{\sigma}, \mathbf{\mu}, A, I)$ |Hàm tạm dừng đặc biệt |
|$w$                |Hoạt động hiện tại sẽ được thực thi |

### Khối (Block)
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
|$B$                |Một khối: $B \equiv (B_H, B_\mathbf{T}, B_\mathbf{U})$ |
|$B_H$              |Header của khối |
|$B_\mathbf{T}$     |Một loạt các giao dịch của khối |
|$B_\mathbf{U}$     |Mảng các hash header của các khối ommer/uncle của khối này. Sau khi chuyển cơ chế đồng thuận sang bằng chứng cổ phần, hiện tại không còn dùng nữa và được đặt thành mảng rỗng |
|$B_\mathbf{R}$     |Biên nhận giao dịch (transaction receipt), $B_\mathbf{R}[i]$ là biên nhận của giao dịch thứ i |
|$D(H)$             |Độ khó của khối có header $H$ |
|$P(H)$             |Khối cha của khối có header $H$ |
|$V(H)$             |Hàm xác thực header của khối |

### Header khối (Block header)
| Ký hiệu         | Mô tả                               |
| --------------- | ---------------------------------------- |
| $H_p$           | **parentHash**: Hash Keccak 256-bit của header block cha, toàn bộ nội dung. |
| $H_o$           | **ommersHash**: Hash Keccak 256-bit của danh sách ommers của block này. Hiện tại không còn dùng nữa và giá trị của nó là hằng số $\texttt{KEC}\big(\texttt{RPL}(())\big)$ do sự thay đổi cơ chế đồng thuận sang bằng chứng cổ phần|
| $H_c$           | **beneficiary**: Địa chỉ 160-bit mà toàn bộ phí ưu tiên thu được từ quá trình đào block này sẽ được chuyển đến (địa chỉ thụ hưởng). |
| $H_r$           | **stateRoot**: Hash Keccak 256-bit của nút gốc của cây (trie) trạng thái, sau khi tất cả các giao dịch được thực thi và các kết quả cuối cùng được áp dụng. |
| $H_t$           | **transactionsRoot**: Hash Keccak 256-bit của nút gốc của cấu trúc cây (trie), đại diện cho tất cả các giao dịch đã được thêm vào phần danh sách giao dịch trong khối. |
| $H_e$           | **receiptsRoot**: Hash Keccak 256-bit của nút gốc của cấu trúc cây (trie), đại diện cho tất cả các biên lai đã được thêm vào của mỗi giao dịch trong phần danh sách giao dịch của khối. |
| $H_b$           | **logsBloom**: Bộ lọc Bloom được tạo ra từ thông tin có thể lập chỉ mục (địa chỉ logger và các log topic) chứa trong mỗi mục log từ biên lai của mỗi giao dịch trong danh sách giao dịch của block này.<br>Trường này chứa một giá trị được tạo ra từ tất cả các log (journal) của giao dịch trong khối đó. Nó được sử dụng để tối ưu hóa quá trình tìm kiếm các sự kiện (events) trong các giao dịch. Mỗi log của một giao dịch có một giá trị Bloom được tạo ra từ các địa chỉ hợp đồng, các topics của log và dữ liệu log. Các giá trị Bloom này từ tất cả các log trong khối sẽ được kết hợp lại theo phép toán Bitwise để tạo ra giá trị cuối cùng của trường `logsBloom` này. |
| $H_d$           | **difficulty**: Giá trị vô hướng tương ứng với độ khó của block này. Hiện tại không còn dùng nữa và được đặt giá trị là 0 do sự thay đổi cơ chế đồng thuận sang bằng chứng cổ phần |
| $H_i$           | **number**: Giá trị vô hướng bằng số lượng block tổ tiên. Block khởi tạo (genesis block) có số lượng là 0. |
| $H_l$           | **gasLimit**: Giá trị vô hướng bằng giới hạn hiện tại của việc tiêu thụ gas cho mỗi block. |
| $H_g$           | **gasUsed**: Giá trị vô hướng bằng tổng gas được sử dụng trong các giao dịch của block này. |
| $H_s$           | **timestamp**: Giá trị vô hướng bằng kết quả hợp lý của hàm `time()` trong Unix khi block này bắt đầu. |
| $H_x$           | **extraData**: Một mảng byte tùy ý chứa dữ liệu liên quan đến block này. Cần phải có độ dài 32-byte hoặc ít hơn. |
| $H_m$           | **prevRandao**: Trước đây là **mixHash** một hash 256-bit bằng chứng, kèm theo **nonce**, rằng một lượng tính toán đủ đã được thực hiện trên block này. Sau khi chuyển cơ chế đồng thuận sang bằng chứng cổ phần, nó là giá trị **RANDAO** mới nhất của trạng thái beacon của khối trước (có thể hiểu là trạng thái hiện tại của hệ thống tại thời điểm cuối cùng của khối trước đó). **RANDAO** là một cơ chế trong Ethereum để tạo số ngẫu nhiên dựa trên dữ liệu từ các người tham gia khác nhau trong hệ thống. Mặt dù vậy, do đặt thù về tính xác định của blockchain, giá trị ngẫu nhiên này vẫn có khả năng bị khống chế hoặc biết trước. |
| $H_n$           | **nonce**: Một hash 64-bit kèm theo **mixHash**, rằng một lượng tính toán đủ đã được thực hiện trên block này. Sau khi chuyển cơ chế đồng thuận sang bằng chứng cổ phần, giá trị này không còn được dùng nữa và được đặt là 0x0000000000000000 |

### Giao dịch (Transaction)
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
| $T_x$           | **type**: Loại giao dịch, xem [EIP-2718](https://eips.ethereum.org/EIPS/eip-2718), nhận 1 trong các giá trị [0, 1, 2] |
| $T_n$           | **nonce**: Nonce của giao dịch, mỗi giao dịch của một địa chỉ cụ thể phải có một giá trị nonce tăng dần. Nonce bắt đầu từ 0 cho giao dịch đầu tiên của địa chỉ đó và tăng lên mỗi khi một giao dịch mới được tạo ra từ địa chỉ đó. Cơ chế này giúp đảm bảo rằng mỗi giao dịch được xác nhận chỉ một lần và không thể bị thực hiện lặp lại một lần nữa (replay attacks).|
| $T_g$           | **gasLimit**: Gas tối đa cho một giao dịch. |
| $T_t$           | **to**: Địa chỉ nhận của giao dịch, bằng $\varnothing$ nếu là giao dịch tạo hợp đồng. |
| $T_v$           | **value**: Giá trị cần chuyển bởi giao dịch. |
| $T_r$, $T_s$    | **r**, **s**: Các giá trị của chữ ký giao dịch, mục đích cung cấp 2 giá trị này là để truy tìm ngược khóa công khai (publicKey) từ chữ ký số, dùng nó cho việc xác minh chữ ký, do là địa chỉ tài khoản thật sự không phải là khóa công khai mà nó chỉ là 1 phần hoặc qua phép biến đổi khác từ khóa công khai. |
| $T_\mathbf{A}$  | **accessList**: Danh sách các địa chỉ đã chạm đến trong quá trình thực hiện giao dịch. Mỗi phần tử trong danh sách là một bộ (tuple) gồm địa chỉ tài khoản và danh sách các key của kho lưu trữ (storage key) $E=(E_a, E_s)$ |
| $T_c$           | **chainId**: Một giá trị vô hướng, là Id của chuỗi nơi mà giao dịch được thực hiện. |
| $T_y$           | **yParity**: Chẵn hoặc lẽ [0, 1] (dương hay âm). Do quá trình truy ngược để tìm khóa công khai từ $T_r$ và $T_s$ sẽ có 2 nghiệm thỏa mãn, 2 nghiệm này đối nhau, nhờ $T_y$ để xác định đúng giá trị cần tìm mà không cần phải tính toán thêm. Xem thêm về đường cong Eliptic và chữ ký số [secp256k1](https://en.bitcoin.it/wiki/Secp256k1) |
| $T_w$           | **w**: Một giá trị vô hướng được tính toán phụ thuộc vào $T_y$, $T_c$, và độ cao khối, xem [EIP-155](https://eips.ethereum.org/EIPS/eip-155). |
| $T_m$           | **maxFeePerGas**: Giá gas tối đa cho giao dịch (tính bằng Wei). |
| $T_f$           | **maxPriorityFeePerGas**: Giá gas ưu tiên tối đa cho giao dịch (tính bằng Wei). |
| $T_p$           | **gasPrice**: Giá gas cho giao dịch. |
| $T_i$           | **init**: Mảng byte không giới hạn kích thước, là mã EVM sẽ thực thi khi tạo hợp đồng và kết quả của việc thực thi này trả về là mã hợp đồng. |
| $T_\mathbf{d}$  | **data**: Dữ liệu đầu vào của cuộc gọi tin nhắn. |
| $S(T)$          | Hàm người gửi - khôi phục địa chỉ người gửi từ giao dịch: $S(T) \equiv \mathcal{B}_{96..255}\big(\mathtt{KEC}\big( \mathtt{ECDSARECOVER}(h(T), T_w, T_r, T_s) \big) \big).$ |

### Biên lai giao dịch (Transation Receipt)
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
|$R$              | Biên lai giao dịch (transaction receipt): $R \equiv (R_x, R_z, R_u, R_b, R_l)$ |
|$R_x$            | Loại giao dịch |
|$R_z$            | Tình trạng của giao dịch |
|$R_u$            | Lượng gas tích lũy đã sử dụng trong giao dịch |
|$R_b$            | Bộ lọc Bloom được tạo ra từ thông tin trong các logs của giao dịch này, là một hash 2048-bit (256-byte). Hash này được tính toán phụ thuộc vào dữ liệu của tập hợp logs của giao dịch |
|$R_l$            | Tập hợp các logs đã được tạo trong suốt quá trình thực thi của giao dịch, $(O_0, O_1, ...)$. |
| $O$             | Một mục log: $O \equiv (O_a, ({O_\mathbf{t}}_0, {O_\mathbf{t}}_1, ...), O_\mathbf{d})$. |
| $O_a$           | Là một bộ (tuple) gồm các địa chỉ của các logger. |
| $O_\mathbf{t}$  | Một topic log 32-byte, có thể $\varnothing$. |
| $O_\mathbf{d}$  | Dữ liệu log cho mục này. |
| $\Upsilon^g$    | Tổng gas sử dụng trong giao dịch này. |
| $\Upsilon^\mathbf{l}$ | Các log được tạo ra bởi giao dịch này. |
| $\Upsilon^z$    | Mã trạng thái của giao dịch này, $z$. |
|$L_R$            | Hàm chuẩn bị dữ liệu cho biên nhận giao dịch R: $L_R(R) \equiv (R_z, R_u, R_b, R_l)$, dữ liệu này dành cho việc mã hóa thành mảng byte theo cấu trúc $\texttt{RLP}$ |

### Những hàm khác
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
| $\ell(\mathbf{x})$ | Phần tử cuối cùng trong dãy $\mathbf{x}$: $\ell(\mathbf{x}) \equiv \mathbf{x}[\lVert \mathbf{x} \rVert - 1]$ |
| $L(n)$          | Hàm "tất cả trừ một phần 64" (all but one 64th): $L(n) \equiv n - \lfloor n / 64 \rfloor$.|
| $L_I\big( (k, v) \big)$ | Biểu diễn của cặp khóa--giá trị trong cây trie: $L_I\big( (k, v) \big) \equiv \big(\texttt{KEC}(k), \texttt{RLP}(v)\big)$ |
| $L_S$           | Hàm suy giảm trạng thái thế giới. Hàm này thao tát trên tập hợp tất cả tài khoản hiện có trên hệ thống, trả về một tập hợp mới gồm các bộ (tuple) khóa và giá trị (key,value) trong đó key là $\texttt{KEC}(a)$ và value là $\texttt{RLP}\big((\sigma[a]_n, \sigma[a]_b, \sigma[a]_s, \sigma[a]_c)\big)$ của bộ trạng thái tài khoản $\sigma[a]$ |
|$L_T$            | Hàm chuẩn bị dữ liệu cho giao dịch $T$, dữ liệu này dành cho việc mã hóa thành mảng byte theo cấu trúc $\texttt{RLP}$ |
|$L_R$            | Hàm chuẩn bị dữ liệu cho biên nhận giao dịch: $L_R(R) \equiv (R_z, R_u, R_b, R_l)$, dữ liệu này dành cho việc mã hóa thành mảng byte theo cấu trúc $\texttt{RLP}$ |
| $M(s, f, l)$    | Hàm mở rộng bộ nhớ. $s$ là đỉnh hiện tại của bộ nhớ; $f$ là điểm bắt đầu ghi; $l$ là số byte cần ghi. |
| $\mathcal{B}$   | Hàm tham chiếu bit sao cho $\mathcal{B}_j(\mathbf{x})$ bằng bit thứ $j$ (đánh chỉ mục từ 0) trong mảng byte $\mathbf{x}$ |
| $\mathtt{EMPTY}(\boldsymbol{\sigma}, a)$ | Một tài khoản $a$ được gọi là $\textit{rỗng}$ khi nó không có mã, nonce bằng không và số dư bằng không, $\boldsymbol{\sigma}[a]_c = \texttt{\small KEC}\big(()\big) \wedge \boldsymbol{\sigma}[a]_n = 0 \wedge \boldsymbol{\sigma}[a]_b = 0$. |
| $\mathtt{DEAD}(\boldsymbol{\sigma}, a)$ | Một tài khoản $a$ được gọi là $\textit{chết}$ khi trạng thái tài khoản không tồn tại hoặc rỗng: $\varnothing \vee \mathtt{EMPTY}(\boldsymbol{\sigma}, a)$. |
| $\mathtt{TRIE}(...)$ | Hash gốc của cây Merkle Patricia được xây dựng từ các đối số của nó. |
| $\mathtt{KEC}(...)$ | Hàm hash Keccak-256 |
| $\mathtt{KEC512}(...)$ | Hàm hash Keccak-512 |
| $\mathtt{RLP}(...)$ | Hàm mã hóa tiền tố đệ quy |
| $\mathtt{PoW}(...)$ | Hàm bằng chứng làm việc |

### Toán hạng và Biểu tượng
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
| $\lVert ... \rVert$ | Độ dài hoặc số lượng phần tử của một mảng/ tập hợp/ bộ/ dãy/ chuỗi. |
| $\wedge$        | Toán tử logic `và`. |
| $\vee$          | Toán tử logic `hoặc`. |
| $\varnothing$   | Tập hợp rỗng. |
| $\cdot$         | Toán tử nối, $(a, b, c, d) \cdot e \equiv (a, b, c, d, e)$, hoặc nhân vô hướng tùy thuộc vào ngữ cảnh. |

### Các ký hiệu khác
| Ký hiệu         | Mô tả                                     |
| --------------- | ----------------------------------------- |
| $\mathbb{B}$    | Tập hợp tất cả các dãy byte. |
| $\mathbb{B}_n$  | Tập hợp tất cả các dãy byte có độ dài $n$ byte: $\mathbb{B}_n = \{ B: B \in \mathbb{B} \wedge \lVert B \rVert = n \}$ |
| $\mathbb{T}$    | Tập hợp các mảng byte và dãy cấu trúc |
| $\mathbb{L}$    | Tập hợp tất cả các cây (tree) - nghĩa là cấu trúc chứ không phải là một lá đơn |
| $\mathbb{Y}$    | Tập hợp các nibbles (4-bit) |
| $\mathbb{O}$    | Tập hợp các bytes (8-bit) |
| $M_{3:2048}$    | Bộ lọc Bloom chuyên biệt |
| $\Lambda(...)$  | Hàm tạo hợp đồng |
| $\Theta(...)$   | Hàm "gọi tin nhắn"/thực thi hợp đồng |
| $\Gamma(B)$     | Trạng thái khởi đầu của block $B$. Thường là $\boldsymbol{\sigma}_i: \mathtt{TRIE}(L_S(\boldsymbol{\sigma}_i)) = {P(B_H)_H}_r$ |
| $\Phi(B)$       | Hàm chuyển tiếp block ánh xạ một block $B$ chưa hoàn chỉnh thành một block hoàn chỉnh $B'$ (thêm vào mixHash, nonce, stateRoot) |
