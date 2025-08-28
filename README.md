## 📝 BÁO CÁO HỆ THỐNG NHẬN DIỆN HÀNH ĐỘNG VÀ ĐẾM SỐ LƯỢNG

### 🎯 TỔNG QUAN
Hệ thống có chức năng nhận diện và đếm các hành động thể dục như **push-up**, **squat**. Cấu trúc bao gồm các thành phần:

- **Truyền và nhận thông tin** giữa Front-end ↔ Back-end.
- **Xử lý thông tin** thông qua các bước:
    - `Preprocess`
    - `Process`
    - `Postprocess`

👉 **Ưu tiên sử dụng Python** cho các hàm xử lý để đảm bảo dễ đọc và dễ bảo trì.

---

### 🖥️ FRONT-END

#### 🔧 Ngôn ngữ: JavaScript

#### 📌 Chức năng:

- **Mở camera** và **truyền các frames** về Back-end.
- **Nhận kết quả đã xử lý** từ Back-end và **hiển thị trực quan** cho người dùng.

> 💡 Lưu ý: Hiện tại dữ liệu nhận là giả. Sẽ được cập nhật khi các nhánh code khác ổn định.

---

### 🛠️ BACK-END

#### 🖥️ Thành phần: Server (API)

#### 📌 Chức năng:

1. **Nhận frames** từ Front-end.
2. **Trích xuất landmarks** từ frames thông qua `MediaPipe`.
3. **Nhận diện hành động** với module `action classification (***AI)`.
4. **Đếm số lượng hành động** tương ứng sau khi nhận diện.
5. **Lưu kết quả** vào `JSON` hoặc định dạng phù hợp.
6. **Gửi dữ liệu đã xử lý** ngược lại Front-end.

---

### 🧠 AI - Nhận Diện Hành Động (action classification)***

#### 🏗️ Quy trình:

1. **Chuẩn bị dữ liệu:**
    - Sử dụng 22 điểm landmarks và 12 góc từ các landmarks đó.
    - Trích xuất `x, y, z` → lưu vào file `windows.h5` (shape: `(30, 78)`).

2. **Xử lý đặc trưng (Feature Engineering):**
    - Đang kiểm thử.

3. **Huấn luyện:**
    - Dùng 2 model trong `model.py`: `LSTM`, `BiLSTM`.

#### 🎯 Kỳ vọng:

| Tập dữ liệu      | F1 Score kỳ vọng |
|------------------|------------------|
| Test set         | > 0.95           |
| Real_easy (video tự quay) | > 0.90           |
| Real_hard (góc quay khó hơn) | > 0.85           |

#### 🔍 Inference:

- Nhận đầu vào là `landmarks`, trả về kết quả dự đoán hành động.
- Tốc độ kỳ vọng: **> 25 FPS**

---

### 👥 PHÂN CÔNG VAI TRÒ

| Thành viên  | Vai trò |
|-------------|---------|
| **Dương**   | Leader, AI, IT Helpdesk |
| **Vinh**    | Tổng hợp dữ liệu cho AI, logic đếm, base JavaScript |
| **Tuấn Anh**| Tổ chức codebase, build nền dự án, cập nhật khi merge |

---

### 📦 KẾ HOẠCH TIẾP THEO

- Sau khi kiểm thử hệ thống ổn định → **Tạo GUI training**:
    - Hỗ trợ bật/tắt hệ thống.
    - Training các model trực quan.

---

### 🧩 NHỮNG ĐIỀU CẦN BỔ SUNG:
...

---


## 📘 ENGLISH VERSION

### OVERVIEW
The system detects and counts physical activities like **push-ups** and **squats**, consisting of:

- **Information transmission** between Front-end ↔ Back-end.
- **Processing pipeline**: `Preprocess → Process → Postprocess`.

> Python is preferred for processing logic to improve readability and maintainability.

---

### FRONT-END

#### Language: JavaScript

#### Functions:

- Open the **camera** and send **video frames** to Back-end.
- Receive processed results and **visualize output** for users.

> ⚠️ Current inputs are mock data for integration testing.

---

### BACK-END

#### Component: Server

#### Functions:

1. **Receive frames** from Front-end.
2. **Extract landmarks** using `MediaPipe`.
3. **Recognize actions** using AI module.
4. **Count actions** based on recognized results.
5. **Save results** to JSON or appropriate format.
6. **Send results** back to Front-end.

---

### AI - Action Classification

#### Data Preparation:

- Use 22 landmarks and 12 derived angles.
- Extract `x, y, z` → stored in `windows.h5` (shape: `(30, 78)`).

#### Feature Engineering:

- Currently under testing.

#### Training Models:

- Models used: `LSTM`, `BiLSTM` in `model.py`.

#### Performance Goals:

| Dataset        | Expected F1 Score |
|----------------|-------------------|
| Test set       | > 0.95            |
| Real_easy      | > 0.90            |
| Real_hard      | > 0.85            |

#### Inference:

- Input: Landmarks → Output: Action.
- Target: **> 25 FPS**

---

### TEAM ROLES

| Member     | Role                         |
|------------|------------------------------|
| Dương      | Leader, AI, IT Helpdesk      |
| Vinh       | Data Collection, JS Logic    |
| Tuấn Anh   | Codebase Structure & Updates |

---

### NEXT STEPS

- Develop **Training GUI**:
    - Toggle system on/off.
    - Train models via GUI.

---

### ADDITIONAL TODOs

---

## 🇯🇵 日本語バージョン

### 概要
このシステムは、**腕立て伏せ（Push-up）**や**スクワット（Squat）**などの運動動作を認識し、回数をカウントします。

- **Front-end ↔ Back-end 間の通信**
- 処理ステップ：`前処理 → 処理 → 後処理`

> 読みやすく保守しやすいように、Pythonでの実装を優先しています。

---

### フロントエンド

#### 使用言語：JavaScript

#### 機能：

- カメラを起動し、**フレームをBack-endに送信**
- 処理済みのデータを受け取り、**可視化表示**

> ⚠️ 現在はモックデータで動作確認中。

---

### バックエンド

#### コンポーネント：サーバー（API）

#### 機能：

1. フロントエンドからのフレームを受信。
2. `MediaPipe`を使用してランドマークを抽出。
3. AIモジュールにより動作を認識。
4. 認識された動作に応じて回数をカウント。
5. 結果を `JSON` や適切な形式で保存。
6. 処理されたデータをフロントエンドに返す。

---

### AI - 動作認識

#### データ準備：

- 22個のランドマーク + 12個の角度を使用。
- 各ランドマークの `x, y, z` を抽出し、`windows.h5` に保存（shape: `(30, 78)`）

#### 特徴量エンジニアリング：

- 現在テスト段階。

#### 学習モデル：

- 使用モデル：`LSTM`、`BiLSTM`（`model.py` 内）

#### 精度の目標：

| データセット               | F1スコア目標     |
|----------------------------|------------------|
| テストセット               | > 0.95           |
| Real_easy（簡単な動画）    | > 0.90           |
| Real_hard（難しい角度の動画）| > 0.85           |

#### 推論：

- 入力：ランドマーク → 出力：動作ラベル
- 目標処理速度：**25FPS以上**

---

### チームメンバーと役割

| メンバー   | 役割                         |
|------------|------------------------------|
| Dương      | リーダー、AI、ITサポート     |
| Vinh       | データ収集、カウントロジック、JavaScript ベースコード |
| Tuấn Anh   | コード構成、プロジェクトベース構築、マージ・更新対応 |

---

### 次のステップ

- システムが安定したら、**トレーニング用GUI**を構築予定：
    - システムの ON/OFF を切り替え可能
    - モデルのトレーニング操作をGUIから実施

---

### 今後の追加事項

---
