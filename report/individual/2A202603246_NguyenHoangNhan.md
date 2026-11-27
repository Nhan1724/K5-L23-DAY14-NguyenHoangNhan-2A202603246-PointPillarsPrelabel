# Báo cáo Day 14 — Nguyễn Hoàng Nhân — 2A202603246

> Sao chép file này thành `report/individual/<MSSV>_<HoTen>.md` (không dấu), ví dụ `2A20260000_NguyenVanAn.md`.

- Mã học viên dùng với `--student`: `2A202603246`
- `seed_tag` trong `frames_A.txt`: `393590736f`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- **Tham số tôi nghĩ giảm công sửa nhiều nhất:** `score_thr` (tăng từ `0.1` lên khoảng `0.4`–`0.5`), tiếp theo có thể cân nhắc `min_points` để lọc các box ít điểm ở xa.
- **Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?):** Ở ngưỡng thấp (`score_thr = 0.1`), mô hình sinh ra khá nhiều box có `score` thấp (khoảng `0.2`–`0.45`) hoặc ít điểm (`npts` nhỏ) nằm rải rác quanh vùng biên/xa tâm, trong khi các box đối tượng chính thường có `score` cao hơn rõ rệt. Do đó mình dự đoán **box thừa (false positive) chiếm ưu thế** hơn so với box sót, nên tăng `score_thr` sẽ loại bỏ nhanh các box nhiễu này và giảm chi phí xóa box đáng kể.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | | | | |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_<ID>/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_<ID>/frames_B.txt --config d14_<ID>/best_config.json --gt d14_<ID>/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
