# Reflection — Lab 19

**Tên:** Nguyễn Thành Vinh - 2A202602889
**Cohort:** K4
**Path đã chạy:** _lite_

---

## Câu hỏi (≤ 200 chữ)

> Trên golden set 50 queries, mode nào thắng ở loại query nào (`exact` /
> `paraphrase` / `mixed`), và tại sao? Khi nào bạn **không** dùng hybrid
> (i.e. khi nào pure BM25 hoặc pure vector là lựa chọn đúng)?

Trên 50 golden queries:
- **`exact`:** BM25 (96.7%) và Hybrid (96.7%) thắng Semantic (88.7%) nhờ khớp chính xác keyword kỹ thuật nguyên văn.
- **`mixed`:** Hybrid thắng tuyệt đối (100.0% vs BM25 97.0%, Semantic 98.5%) vì RRF ($k=60$) kết hợp hài hòa cả tín hiệu từ vựng lẫn ngữ cảnh ngữ nghĩa.
- **`paraphrase`:** BM25 (33.3%) và Hybrid (32.0%) dẫn trước do mô hình `bge-small-en` huấn luyện trên tiếng Anh; với Tiếng Việt, cần chuyển sang `bge-m3` để semantic bứt phá.
- **Tổng thể:** Hybrid thắng trung bình (78.6% vs BM25 77.8%, Vector 73.2%).

**Khi nào KHÔNG dùng hybrid:**
1. **Pure BM25:** Khi truy vấn là định danh chuẩn xác (mã SKU, ID đơn hàng, error code, log trace, tên riêng) hoặc tài nguyên CPU/RAM cực kỳ hạn chế không thể chạy model embedding.
2. **Pure Vector:** Khi tìm kiếm đa phương thức (ảnh, âm thanh), truy vấn cross-lingual (hỏi tiếng Việt tìm tài liệu tiếng Anh), hoặc câu hỏi mang tính khái niệm trừu tượng không có keyword trùng khớp.

---

## Điều ngạc nhiên nhất khi làm lab này

Filtered search dạng post-filter sập recall về 0% khi selectivity ~4% (bẫy recall), trong khi filtered-ANN giữ vững 100% nhờ đẩy vị từ lọc vào sâu cấu trúc duyệt index.

---

## Bonus challenge

- [ ] Đã làm bonus (xem `bonus/`)
- [ ] Pair work với: _<tên đồng đội nếu có>_
