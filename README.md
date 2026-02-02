# Progress Test 2 - Hotel Booking System UML Design

## 📋 Thông tin bài tập

**Môn học**: Phân tích và Thiết kế Hệ thống  
**Đề tài**: Thiết kế hệ thống đặt phòng khách sạn (Hotel Booking System)  
**Giảng viên**: traltb@fe.edu.vn

## 🎯 Mục tiêu

Thiết kế một module đặt phòng khách sạn áp dụng:
- Mô hình 3 lớp (Controller - Service - Repository)
- UML Class Diagram với các mối quan hệ: Composition, Aggregation, Association, Dependency, Realization
- SOLID Principles
- PlantUML để documentation

## 📁 Cấu trúc thư mục

```
progress-test-2/
├── README.md                      # File này
├── Progress_Test_2.docx          # Báo cáo hoàn chỉnh (Phần 1, 2, 3)
├── HotelBookingSystem.puml       # PlantUML source code
├── SodoUML.png                   # Sơ đồ UML (xuất từ PlantUML hoặc StarUML)
├── generate-doc.js               # Script tạo file Word
├── .gitignore                    # Git ignore configuration
└── docs/                         # Thư mục tài liệu bổ sung (optional)
```

## 📚 Nội dung hoàn thành

### ✅ Phần 1: Lý thuyết (9 câu hỏi)

1. **Phân tích Lifecycle**: Guest vs Booking, Hotel vs Room
2. **Interface Pattern**: Tại sao cần IBookingService?
3. **Multiplicity**: Bội số giữa Booking và Room
4. **Method Parameters**: Tham số cho makeReservation()
5. **Dependencies**: Tương tác trong calculateTotal()
6. **Design Evolution**: Xử lý khi xóa Guest nhưng giữ Booking
7. **Repository Pattern**: Lợi ích khi chuyển đổi database
8. **Aggregation**: Mối quan hệ Booking - Invoice
9. **Composition**: Mối quan hệ Booking - Payment

### ✅ Phần 2: Sơ đồ Class Diagram

Sơ đồ bao gồm:
- **Controller Layer**: BookingController
- **Service Layer**: IBookingService, BookingService
- **Repository Layer**: IBookingRepository, IRoomRepository
- **Domain Entities**: Hotel, Room, RoomType, Guest, Booking, BookingStatus

### ✅ Phần 3: PlantUML Implementation

Code PlantUML với:
- ✓ Linetype ortho
- ✓ Stereotypes (<<Controller>>, <<Service>>, <<Repository>>)
- ✓ 3+ attributes và 2+ methods cho mỗi class
- ✓ Visibility modifiers (+/-)
- ✓ Đầy đủ relationships: Realization, Composition, Association, Dependency
- ✓ Multiplicity rõ ràng
- ✓ Notes giải thích design decisions

## 🚀 Cách sử dụng

### 1. Clone repository

```bash
git clone https://github.com/[username]/progress-test-2.git
cd progress-test-2
```

### 2. Xem sơ đồ UML

**Cách 1: Sử dụng IntelliJ IDEA**
1. Cài đặt PlantUML Integration plugin
2. Mở file `HotelBookingSystem.puml`
3. Xem preview ở bên phải

**Cách 2: Command line**
```bash
# Cài đặt PlantUML (Ubuntu/Debian)
sudo apt-get install plantuml graphviz

# Generate PNG
plantuml HotelBookingSystem.puml

# Output: HotelBookingSystem.png
```

**Cách 3: Online**
1. Truy cập http://www.plantuml.com/plantuml/
2. Copy nội dung file `HotelBookingSystem.puml`
3. Paste vào editor

### 3. Tạo lại file Word (nếu cần)

```bash
npm install -g docx
node generate-doc.js
```

## 🏗️ Kiến trúc hệ thống

### Layered Architecture

```
┌─────────────────────────────────────┐
│      Controller Layer               │
│   - BookingController                │
└──────────────┬──────────────────────┘
               │ uses (Dependency)
               ↓
┌─────────────────────────────────────┐
│      Service Layer                   │
│   - IBookingService (Interface)      │
│   - BookingService (Implementation)  │
└──────────────┬──────────────────────┘
               │ uses (Dependency)
               ↓
┌─────────────────────────────────────┐
│      Repository Layer                │
│   - IBookingRepository               │
│   - IRoomRepository                  │
└──────────────┬──────────────────────┘
               │ manages
               ↓
┌─────────────────────────────────────┐
│      Domain Entities                 │
│   - Hotel, Room, RoomType            │
│   - Guest, Booking, BookingStatus    │
└─────────────────────────────────────┘
```

### Các mối quan hệ chính

| Từ | Đến | Loại | Multiplicity | Giải thích |
|---|---|---|---|---|
| Hotel | Room | Composition (*--) | 1 → 0..* | Hotel quản lý Rooms. Xóa Hotel → xóa Rooms |
| Room | RoomType | Association (--) | 0..* → 1 | Nhiều Rooms có cùng type |
| Guest | Booking | Association (--) | 1 → 0..* | Guest có nhiều Bookings |
| Booking | Room | Association (--) | 0..* ↔ 1..* | Booking gồm nhiều Rooms |
| BookingService | IBookingService | Realization (\<\|..) | - | Service implements Interface |
| BookingController | IBookingService | Dependency (..>) | - | Controller uses Service |

## 🎓 Kiến thức áp dụng

### SOLID Principles

1. **Single Responsibility**: Mỗi class có một nhiệm vụ rõ ràng
2. **Open/Closed**: Interface cho phép mở rộng mà không sửa code
3. **Liskov Substitution**: BookingService có thể thay thế bởi bất kỳ implementation nào của IBookingService
4. **Interface Segregation**: Interfaces nhỏ, tập trung (IBookingService, IBookingRepository)
5. **Dependency Inversion**: Phụ thuộc vào abstractions (interfaces), không phụ thuộc vào concrete classes

### Design Patterns

- **Repository Pattern**: Tách logic data access
- **Dependency Injection**: Controller nhận IBookingService qua constructor
- **Service Layer Pattern**: Business logic tập trung ở Service

## 📊 Entities và Attributes

### Hotel
- hotelId: Long
- name: String
- address: String
- starRating: Integer
- phoneNumber: String
- email: String
- isActive: Boolean

### Room
- roomId: Long
- roomNumber: String
- floor: Integer
- isAvailable: Boolean
- maxOccupancy: Integer
- description: String

### Guest
- guestId: Long
- firstName: String
- lastName: String
- email: String
- phoneNumber: String
- loyaltyPoints: Integer
- registrationDate: Date

### Booking
- bookingId: Long
- checkInDate: Date
- checkOutDate: Date
- totalAmount: BigDecimal
- status: BookingStatus
- createdAt: Timestamp
- updatedAt: Timestamp

## 🔧 Technologies

- **UML Tool**: PlantUML, StarUML
- **Documentation**: Node.js + docx library
- **Version Control**: Git
- **Diagram Format**: PNG, SVG

## 📖 Tài liệu tham khảo

- [PlantUML Class Diagram Guide](https://plantuml.com/class-diagram)
- [UML Relationships](https://www.uml-diagrams.org/association.html)
- [SOLID Principles](https://en.wikipedia.org/wiki/SOLID)
- [Repository Pattern](https://martinfowler.com/eaaCatalog/repository.html)

## 👤 Tác giả

- **MSSV**: DE180336
- **Họ tên**: Nguyễn Hữu Triết
- **Lớp**: SE18D05
- **Email**: nhuutriet04@gmail.com

## 📝 License

Bài tập thuộc về sinh viên và FPT University. Chỉ sử dụng cho mục đích học tập.

---

⭐ **Lưu ý**: File `Progress_Test_2.docx` chứa toàn bộ câu trả lời chi tiết cho cả 3 phần. Đây là deliverable chính của bài tập.
