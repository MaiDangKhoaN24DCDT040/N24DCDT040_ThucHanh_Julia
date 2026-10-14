# Thực hành Cấu trúc dữ liệu và giải thuật bằng Julia

- Họ tên: Mai Đăng Khoa
- MSSV: N24DCDT040
- Lớp: D24CQDT01-N
- Ngày thực hành: 09/10/2026
- Môi trường đã chạy: Windows 11, Julia 1.12.7

## Nội dung

Ứng dụng điều phối giao đơn: đọc CSV → sắp xếp và tra cứu
→ BFS tính đường đi và chi phí → quy hoạch động chọn đơn
→ giao và hoàn tác → xuất CSV.

Đã hoàn thiện bốn hàm trong khung của giảng viên:
merge_sort, binary_search, bfs_routes và knapsack.

Mỗi đơn là một chuyến riêng từ kho 1 đến điểm giao rồi về kho.
Chi phí = 2 × số cạnh đường BFS + thời gian phục vụ.
Mục tiêu là tối đa tổng lợi ích trong ngân sách; mỗi đơn chọn tối đa một lần.

## Các tệp

- TH_2026_10_09_Sinh_vien.jl: code lõi và bốn hàm đã hoàn thiện.
- TH_2026_10_09_Kiem_thu.jl: bộ kiểm thử của giảng viên.
- TH_2026_10_09_Pluto.jl: notebook gọi cùng code lõi, kèm giải thích.
- ket_qua_kiem_thu.txt: đầu ra kiểm thử thực tế.
- data/MINI001/: hai CSV đầu vào và CSV kết quả mẫu.
- data/N24DCDT040/: hai CSV đầu vào và CSV kết quả cá nhân.

## Cách chạy lại

Tải repository bằng Code → Download ZIP và giải nén.
Mở terminal trong thư mục chứa ba tệp .jl.
Máy cần gọi được lệnh julia; code lõi chỉ dùng Julia Base.

### 1. Đọc dữ liệu và kiểm thử toàn bộ

```text
julia TH_2026_10_09_Sinh_vien.jl --data
julia TH_2026_10_09_Kiem_thu.jl --phase=all
```

Có thể kiểm riêng từng pha bằng --phase=data, sort, search, bfs, dp hoặc app.

### 2. Chạy ứng dụng mẫu

```text
julia TH_2026_10_09_Sinh_vien.jl --mini
```

Kết quả được xuất tại data/MINI001/ket_qua.csv.

### 3. Chạy notebook

```text
julia TH_2026_10_09_Pluto.jl
```

Notebook đã bật READ_DATA và RUN_APP, gọi cùng code lõi.
Có thể mở bằng Pluto hoặc chạy trực tiếp bằng Julia như trên.

### 4. Chạy dữ liệu cá nhân

```text
julia TH_2026_10_09_Sinh_vien.jl --data N24DCDT040
julia TH_2026_10_09_Sinh_vien.jl N24DCDT040 --demo
```

Kết quả được xuất tại data/N24DCDT040/ket_qua.csv.
Giữ nguyên cấu trúc thư mục data khi tải và chạy.

## Kết quả thực tế

Bộ kiểm thử đạt 60/60 phép kiểm tra:
data 12, sort 8, search 5, bfs 7, dp 12, app 16.

MINI001: ngân sách 8, chọn ID 1 và 2.
Giao hết dùng thời gian 8, nhận lợi ích 14.
Giao ID 1 rồi hoàn tác khôi phục hàng đợi [1,2] và hai tổng về 0.

Dữ liệu N24DCDT040: 8 đơn, ngân sách 28.
Thứ tự giao được chọn [1,6,5,2].
Giao hết dùng thời gian 24, nhận lợi ích 42.

CSV kết quả được xuất sau chuỗi thao tác:
lập kế hoạch → giao một đơn → hoàn tác → giao lại và giao hết.

## Giới hạn
BFS tối thiểu số cạnh trên đồ thị không trọng số.
Tham lam theo tỷ số lợi ích/chi phí không luôn tối ưu cho ba lô 0/1.
BST tra cứu theo chiều cao cây, không mặc nhiên O(log n).
Ứng dụng không tối ưu một chuyến giao nhiều điểm.
