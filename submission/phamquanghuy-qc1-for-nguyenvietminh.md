# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): nguyenvietminh        Người kiểm (học viên): Phạm Quang Huy (phamquanghuy)
Ngày: 2026-11-21                               Phiên bản guideline: Road v1.0
File được kiểm (tên + `revision` trong manifest): `nguyenvietminh-front.zip`, `nguyenvietminh-fisheye.zip`, revision 1 (sha256 của cả hai file khớp manifest)
Số ảnh kiểm: 6 (A01, A04, A07, A08, B01, B07) (+ 0 ảnh thêm: lô không có A13–A16, B09–B12)   Số nhãn đã kiểm (shape + tag): 80 (56 shape + 24 tag)

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 1 | nặng (camera) / nhẹ (tag khác) |
| QC1-02 đủ L1, R1 | bỏ sót | 5 | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 14 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 14 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 6 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 14 | 2 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 15 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 14 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 26 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 12 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 9 | 1 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Cách đếm "Số mục kiểm": QC1-01 là số tag (4 × 6 ảnh); QC1-02 là số ảnh cần có L1/R1 (5 ảnh front, fisheye_front, fisheye_rear); QC1-03, 04, 06 là số lane (14); QC1-05 là số lane vạch đứt (6); QC1-07 là drivable, crosswalk và road_curb ở ảnh front (15); QC1-08 là số đèn (14); QC1-09 là đèn và biển (26); QC1-10 là số biển (12); QC1-11 là mọi shape ở B01, B07 (9); QC1-12 là 2 file zip.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A08 | lane (thiếu, phía trái làn) | nặng | Bên trái làn thấy rõ hai vạch trắng liền chạy về điểm tụ, nhưng không có lane nào được gán ở phía trái, nên thiếu L1. Gần xe hơn còn có một vạch sơn mòn đứt quãng (khoảng (262,420) tới (468,322)), nhiều khả năng là L1 |
| 2 | QC1-06 | A04 | lane#3@(719,535), R1 | chính | Gán `style = solid`, nhưng vạch giữa làn mình và làn phải là vạch đứt (các vệt cách nhau rõ ở y ≈ 360–540). Phải là `dashed` |
| 3 | QC1-06 | B07 | lane#4@(972,271), other | chính | Gán `style = solid`, nhưng ảnh là các vệt sơn trắng rời nhau. Phải là `dashed` |
| 4 | QC1-11 | B07 | road_curb#3@(100,490) | chính | Polyline gập ngược: lên tới (164,367) rồi quay xuống (147,436) và đi lên lại. Đoạn gập không nằm trên mép vỉa |
| 5 | QC1-01 | A07 | tag weather | nhẹ | Gán `clear`, nhưng mặt đường ướt rõ và kính có giọt nước. Theo guideline là `rain` |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A07 | Sát chân dải bê tông bên trái có một vạch trắng mờ (khoảng (260,425) tới (440,360)). Vạch này có tính là L1 thấy được không? Lô hiện không có L1 (lint báo QC1-02) và vùng `direct` kéo tới tận chân dải bê tông | |
| A04, A08, B07 | Trời xám trắng, nhiều mây, đường khô nhưng gán `weather = clear`. Có tính là `overcast` không? | |
| B07 | Bảng kế hoạch B07 chỉ yêu cầu crosswalk + road_curb, lô có thêm một polygon `drivable direct`. Có tính là nhãn thừa (QC1-07) không? | |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 3 / 80 nhãn = 3,75 %   Lỗi nhẹ: 1   Ca chờ lead: 3
Quyết định (Release / Hold / Rework): **Rework**
Lý do (theo luật của phiếu): còn 1 lỗi nặng (QC1-02 ở A08, thiếu L1 khi bên trái có vạch nhìn thấy được). Theo luật, có lỗi nặng là Rework, không phụ thuộc tỉ lệ lỗi chính (3,75 %, dưới ngưỡng 5 %). Ba ca mơ hồ không làm đổi quyết định nên không chọn Hold.

Ghi chú ngoài mẫu (không tính vào tỉ lệ): `road_check lint` trên cả 20 ảnh còn báo thiếu L1/R1 ở A05 (cả hai), A06 (R1), A09 (R1). A05 và A09 nhiều khả năng đúng là không có vạch. A06 bên phải có một vạch đứt trắng ở khoảng (1050–1250, 560–600), bạn nên xem lại. Lint cũng báo 5 biển thấp hơn 8 px ở A10 (không bắt buộc).

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
