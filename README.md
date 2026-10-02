# 🍄 Mario Forensic Lab: Logic-First Game Design (Thiết kế Game đặt Logic lên hàng đầu)

Chào mừng bạn đến với **Mario Forensic Lab**! Trong workshop này, bạn sẽ không chỉ học cách viết code, bạn sẽ học cách trở thành một **Software Architect** (Kiến trúc sư Phần mềm).

Thay vì xây dựng đồ họa ngay từ ngày đầu tiên hoặc gõ từng dòng code, chúng ta sử dụng phương pháp tiếp cận **Logic-First & Code Forensics** (Ưu tiên Logic & Phân tích/Điều tra Mã nguồn). Bạn sẽ thiết kế cơ chế trò chơi, hướng dẫn Generative AI xây dựng cơ chế hoạt động cơ bản, và sau đó thực hiện dịch ngược để hiểu và giải thích cách thức hoạt động của logic ngôn ngữ C bên dưới. Khi logic đã ổn trong giao diện dòng lệnh, bạn sẽ tạo giao diện cho nó bằng một giao diện đồ họa sử dụng thư viện **Raylib**.

---

## 🎮 Final Game Preview

Dưới đây là bản xem trước của ứng dụng hoàn chỉnh mà bạn sẽ thiết kế, xác minh logic và tạo giao diện bằng Raylib trong workshop:

![Mario Game](https://media.giphy.com/media/p0KEKXBzvuwtv8JYVb/giphy.gif)

---

## 🧠 What You Will Learn (Những gì bạn sẽ học)

Thông qua workshop thực hành này, bạn sẽ kết nối kiến thức lý thuyết từ các khóa học đại học trực tiếp vào (kỹ thuật phần mềm thực tế:

- **Structural C Programming (Lập trình C cấu trúc):** Thành thạo `structs` (cấu trúc) để quản lý dữ liệu entity (thực thể), mảng 2 chiều cho ma trận không gian thế giới, vòng lặp và kiến trúc mã nguồn theo mô-đun.
- **Applied Mathematics & Physics (Toán học & Vật lý ứng dụng):** Chuyển đổi hình học tọa độ, công thức khoảng cách Euclid hay Manhattan, và boolean logic gates (cổng logic đúng/sai) thành phát hiện va chạm theo thời gian thực và tầm nhìn của NPC (nhân vật máy).
- **Finite State Machines (FSM - Máy trạng thái hữu hạn):** Thiết kế các mô hình hành vi AI (ví dụ như trạng thái tuần tra và truy đuổi của Bowser).
- **AI Collaboration & Code Forensics (Cộng tác với AI & Điều tra Mã nguồn):** Học kỹ thuật đặt câu lệnh để hướng dẫn AI hoạt động như một lập trình viên đồng hành, và phát triển các kỹ năng audit (kiểm tra) cần thiết để đọc, trace (theo dõi luồng chạy) và refactor (tái cấu trúc/làm sạch) mã nguồn có sẵn.
- **Digital Craftsmanship (Nghệ nhân kỹ thuật số):** Trải nghiệm niềm vui khi xây dựng một ứng dụng nguyên bản, đầy đủ chức năng từ thiết kế đặc tả thiết kế cho đến sản phẩm cuối cùng.

---

## 🛠️ Development Tools Installation (Cài đặt công cụ phát triển)

Vui lòng cài đặt các công cụ dưới đây **trước Buổi 1 (Session 1)** theo hướng dẫn dành cho hệ điều hành của bạn.

### 1. Thiết lập trình biên dịch (Compiler) & Thư viện đồ họa Raylib

#### 🪟 Windows (MSYS2 + MinGW-w64)

1. Tải về và chạy bộ cài đặt từ [msys2.org](https://www.msys2.org/) (sử dụng đường dẫn mặc định `C:\msys64`).
2. Mở **MSYS2 UCRT64** từ Start Menu và cài đặt GCC, Make và Raylib:

```bash
pacman -Syu
pacman -S mingw-w64-ucrt-x86_64-gcc mingw-w64-ucrt-x86_64-make mingw-w64-ucrt-x86_64-raylib

```

3. Thêm GCC vào biến môi trường PATH hệ thống (system PATH):

- Nhấn `Win + R`, nhập `sysdm.cpl`, rồi nhấn **Enter**.
- Vào mục **Advanced (Nâng cao)** > **Environment Variables (Biến môi trường)** > nhấp đúp vào `Path` bên dưới mục System variables (Biến hệ thống).
- Nhấp vào **New**, thêm `C:\msys64\ucrt64\bin`, và nhấn **OK**.
- Khởi động lại các cửa sổ terminal đang mở và kiểm tra lại bằng lệnh: `gcc --version`

#### 🍎 macOS (Homebrew + Apple Clang)

1. Cài đặt Xcode Command Line Tools trong Terminal:

```bash
xcode-select --install

```

2. Cài đặt Homebrew (nếu chưa cài đặt):

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

```

3. Cài đặt Raylib:

```bash
brew install raylib

```

#### 🐧 Linux (Ubuntu / Debian)

Cài đặt GCC, Make, Git và Raylib kèm theo các header file phát triển (development headers):

```bash
sudo apt update
sudo apt install -y build-essential git libraylib-dev libasound2-dev libx11-dev libxrandr-dev libxi-dev libgl1-mesa-dev libglu1-mesa-dev libxcursor-dev libxinerama-dev

```

---

### 2. Thiết lập các công cụ chung

- **Git CLI:** Tải về và cài đặt từ [git-scm.com](https://git-scm.com/).
- **Visual Studio Code:** Tải về từ [code.visualstudio.com](https://code.visualstudio.com/).
  - Extension (tiện ích mở rộng) đề xuất: **C/C++** (do Microsoft phát triển) và **C/C++ Compile Run** hoặc **CMake Tools**.
- **Claude Desktop / AI Assistant (Trợ lý AI):** Tải về từ [claude.ai/download](https://claude.ai/download) hoặc truy cập nền tảng được phân công.

---

## 🚀 Bước 3: Clone Repository & Xác nhận thiết lập

Sau khi đã cài đặt xong các công cụ, hãy clone repository này và kiểm tra môi trường biên dịch của bạn bằng tệp `test_raylib.c` đi kèm.

1. Mở Terminal hoặc Command Prompt và di chuyển đến thư mục làm việc (workspace):

```bash
cd path/to/your/projects-folder

```

2. Clone kho lưu trữ này:

```bash
git clone https://github.com/geu-pit/mario-forensic-workshop.git

```

3. Truy cập vào thư mục của repository:

```bash
cd mario-forensic-workshop

```

### 🧪 Environment Verification (Kiểm tra môi trường)

Biên dịch (compile) và chạy tệp `test_raylib.c` bằng lệnh phù hợp với hệ điều hành của bạn:

- **Windows (Command Prompt / PowerShell):**

```cmd
gcc test_raylib.c -o test_raylib.exe -lraylib -lopengl32 -lgdi32 -lwinmm
.\test_raylib.exe

```

- **macOS (Terminal):**

```bash
gcc test_raylib.c -o test_raylib -lraylib -framework OpenGL -framework Cocoa -framework IOKit -framework CoreVideo
./test_raylib

```

- **Linux (Terminal):**

```bash
gcc test_raylib.c -o test_raylib -lraylib -lGL -lm -lpthread -ldl -lrt -lX11
./test_raylib

```

Nếu một cửa sổ đồ họa hiện lên hiển thị một hình vuông màu đỏ cùng thông báo thành công, môi trường của bạn đã sẵn sàng 100% cho Buổi 1!

---

## 📅 Workshop Overview at a Glance (Tổng quan Nhanh về Khóa học)

| Session (Buổi) | Focus Area (Nội dung Trọng tâm)              | Core Objective (Mục tiêu Cốt lõi)                                                       |
| -------------- | -------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Session 1**  | Matrix & Hero (Ma trận & Nhân vật chính)     | Xây dựng grid, di chuyển Mario bằng phím WASD, và boundary logic (logic giới hạn biên). |
| **Session 2**  | Predator & Key (Kẻ săn mồi & Chìa khóa)      | Triển khai logic truy đuổi theo FSM của Goomba và cơ chế mở khóa Cổng-Chìa khóa.        |
| **Session 3**  | Raylib UI Integration (Tích hợp UI Raylib)   | Kết nối logic xử lý trên dòng lệnh sang một cửa sổ đồ họa.                              |
| **Session 4**  | Independent Architect (Kiến trúc sư Độc lập) | Thiết kế và phát triển một tựa game nguyên bản của riêng bạn sử dụng AI.                |
| **Session 5**  | Finish (Hoàn thiện)                          | Debug code và showcase dự án của bạn.                                                   |

---
