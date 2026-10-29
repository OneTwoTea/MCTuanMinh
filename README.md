# Hướng dẫn thêm, thay ảnh và video

Trang web gồm một file duy nhất: `index.html`. Bạn không cần cài đặt hay build gì. Sửa xong, lưu lại rồi mở `index.html` bằng trình duyệt (hoặc tải lại trang) là thấy thay đổi.

## Thư mục

```
Teamp_Minh/
├── index.html    ← trang web, chỉ sửa file này
├── img/          ← ảnh đang dùng trên trang
├── video/        ← video đang dùng trên trang
└── assets/       ← kho ảnh/video gốc, trang KHÔNG dùng trực tiếp
```

Muốn dùng một file trong `assets/` thì **chép** nó sang `img/` hoặc `video/`, đổi sang tên dễ nhớ, rồi làm theo các bước bên dưới.

## Quy tắc đặt tên file

- Viết thường, không dấu, không khoảng trắng, nối bằng dấu gạch ngang: `nh-6.jpg`, `le-vu-quy.mp4`.
- Tiền tố đang dùng:

  | Tiền tố | Nơi hiển thị |
  |---|---|
  | `nh-` | Dịch vụ: MC nhà hàng, khách sạn |
  | `ah-` | Dịch vụ: MC lễ ăn hỏi |
  | `tg-` | Dịch vụ: MC lễ tư gia |
  | `vow-` | Dịch vụ: MC lễ Vow |
  | `fb-` | Phản hồi khách hàng (ảnh chụp tin nhắn) |

- Đường dẫn trong `index.html` phân biệt chữ hoa, chữ thường khi đưa lên host: `Nh-6.JPG` khác `nh-6.jpg`.

## Chuẩn bị file

**Ảnh**
- Định dạng `.jpg` (ảnh chụp) hoặc `.png` (ảnh chụp màn hình).
- Cạnh dài khoảng **1600px**, dung lượng **dưới 400 KB**. Có thể nén bằng [squoosh.app](https://squoosh.app) hoặc [tinyjpg.com](https://tinyjpg.com).
- Ảnh trong dải dịch vụ được cắt theo khung dọc **3:4**, nên ưu tiên ảnh dọc và để nhân vật ở giữa.

**Video**
- Định dạng `.mp4` (H.264), dài dưới 1 phút, dung lượng **dưới 15 MB**.
- Video dọc 9:16 hoặc 3:4 hiển thị đẹp nhất (khung sẽ cắt phần thừa).
- Nên có một ảnh bìa (poster) `.jpg` cắt từ video, để khung không bị đen trước khi bấm phát.

## 1. Thêm ảnh vào một dịch vụ

Mỗi dịch vụ có một dải ảnh vuốt ngang (`<div class="rail" ...>`). Tìm dịch vụ cần thêm theo tiêu đề `<h3>` trong `index.html`, ví dụ `MC lễ ăn hỏi`:

```html
<div class="rail" tabindex="0" aria-label="Ảnh lễ ăn hỏi">
  <div><button class="shot" type="button"><img src="img/ah-2.jpg" alt="MC mặc vest kem đứng trước phông chữ Hỷ đỏ" loading="lazy"></button></div>
  <div><button class="shot" type="button"><img src="img/ah-1.jpg" alt="MC chụp ảnh bên mâm quả lễ ăn hỏi" loading="lazy"></button></div>
</div>
```

Các bước:
1. Chép ảnh vào `img/`, ví dụ `img/ah-3.jpg`.
2. Sao chép nguyên một dòng `<div><button class="shot" ...>...</div>` rồi dán vào vị trí muốn hiển thị (dòng đầu tiên sẽ hiện đầu tiên).
3. Sửa `src` thành tên file mới và `alt` thành mô tả ngắn nội dung ảnh:

```html
  <div><button class="shot" type="button"><img src="img/ah-3.jpg" alt="Hai họ trao mâm quả trong lễ ăn hỏi" loading="lazy"></button></div>
```

Ảnh mới tự động bấm được để phóng to, không cần sửa gì thêm.

> **`alt` là gì?** Là câu mô tả ảnh cho người dùng trình đọc màn hình và cho Google. Viết bằng tiếng Việt có dấu, mô tả đúng điều thấy trong ảnh. Không để trống.

## 2. Thêm video vào một dịch vụ

Video nằm trong cùng dải với ảnh, như mục MC nhà hàng:

```html
<div><span class="tag">Video</span><video src="video/nha-hang.mp4#t=0.1" controls playsinline preload="metadata" aria-label="Video MC Tuấn Minh dẫn tiệc tại nhà hàng"></video></div>
```

Các bước:
1. Chép video vào `video/`, ví dụ `video/an-hoi.mp4`.
2. Dán dòng sau vào dải của dịch vụ cần thêm (thường đặt đầu tiên):

```html
<div><span class="tag">Video</span><video src="video/an-hoi.mp4#t=0.1" controls playsinline preload="metadata" aria-label="Video MC dẫn lễ ăn hỏi tại tư gia"></video></div>
```

- `#t=0.1` ở cuối tên file giúp trình duyệt lấy khung hình đầu làm ảnh bìa. Nếu có ảnh bìa riêng, bỏ `#t=0.1` và thêm `poster="img/an-hoi-poster.jpg"`.
- Sửa `aria-label` thành mô tả ngắn nội dung video.
- **Đừng** bọc video trong `<button class="shot">`: nút đó chỉ dành cho ảnh.

## 3. Thêm ảnh phản hồi khách hàng

Tìm `<div class="rail reviews"` trong mục **Phản hồi**, rồi thêm dòng:

```html
<div><button class="shot" type="button"><img src="img/fb-6.jpg" alt="Tin nhắn khách cảm ơn MC sau tiệc cưới" loading="lazy"></button></div>
```

Ảnh phản hồi được giữ nguyên tỉ lệ (không cắt), nên dùng ảnh chụp màn hình gốc. Nhớ che số điện thoại, tên Zalo/Facebook của khách nếu họ chưa đồng ý công khai.

## 4. Thay ảnh hoặc video đang có

Cách đơn giản nhất: **ghi đè file cũ bằng file mới cùng tên** (ví dụ thay `img/hero.jpg`). Không cần sửa `index.html`, chỉ nên cập nhật `alt` nếu nội dung ảnh khác.

Các ảnh và video cố định trên trang:

| File | Vị trí | Lưu ý |
|---|---|---|
| `img/hero.jpg` | Ảnh lớn đầu trang | Khung dọc vòm cong, nên để mặt ở 1/5 phía trên ảnh |
| `img/about.jpg` | Mục Giới thiệu | Khung dọc 4:5 |
| `img/thanks.jpg` | Thẻ Liên hệ cuối trang | Khung ngang 3:2 trên điện thoại |
| `video/rot-gao.mp4` + `img/rotgao.jpg` | Mục Vì sao chọn mình | Video dọc 9:16; `rotgao.jpg` là ảnh bìa |

Nếu ảnh đầu trang bị cắt mất mặt, tìm dòng `.hero-media img` trong phần `<style>` và chỉnh giá trị thứ hai của `object-position` (ví dụ `50% 18%` → `50% 30%` để lấy phần ảnh thấp hơn). Với các ảnh khác, cách dễ nhất là tự cắt ảnh trước cho nhân vật nằm giữa.

## 5. Xóa ảnh hoặc video

Xóa nguyên dòng `<div>...</div>` chứa ảnh/video đó trong `index.html`. Sau đó có thể xóa file trong `img/` hoặc `video/` nếu không dùng nữa.

## Kiểm tra sau khi sửa

- [ ] Mở `index.html` bằng trình duyệt: ảnh/video mới hiện đúng chỗ, không có khung trống.
- [ ] Bấm vào ảnh mới: ảnh phóng to, bấm × hoặc phím Esc để đóng.
- [ ] Bấm phát video: chạy được, có tiếng.
- [ ] Thu nhỏ cửa sổ cỡ điện thoại (hoặc F12 → biểu tượng điện thoại): dải ảnh vuốt ngang được.

Khung trống thường do **sai tên file** (thừa khoảng trắng, sai đuôi `.jpg`/`.jpeg`, sai chữ hoa) hoặc **file chưa nằm đúng thư mục**.
