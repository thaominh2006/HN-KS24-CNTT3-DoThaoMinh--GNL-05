Câu 1:
- Lỗi 1: Race condition khi kiểm tra sĩ số: hai request cùng đọc enrolledCount = capacity - 1, cùng qua điều kiện <, rồi cùng tăng. lớp bị vượt sĩ số
- Cách khắc phục: khóa dòng khi đọc, hoặc dùng @Version hoặc dùng câu lệnh cập nhật nguyên tử.
- Lỗi 2: Tin tưởng studentId từ client: kẻ tấn công sửa studentId trong request để đăng kí hoặc chiếm chỗ thay sinh viên khác.
- Cách khắc phục: lấy danh tính từ phiên đăng nhp, không nhận từ body
- Lỗi 3: Không kiểm tra đăng ký trùng: một sinh viên bấm nhiều lần hoặc gửi script, mỗi lần tăng enrolledCount và tạo thêm bản ghi, chiếm hết chỗ của người khắc.
- Cách khắc phục: kiểm tra tồn tại và thêm unique constraint
- Lỗi 4: Thiếu @Transactional
Câu 3:
- đó là race condition. khi nhiều sinh viên cùng đăng ký một lớp còn ít chỗ, nhiều request đồng thời cùng đọc một giá trị enrolledCount và cùng vượt qua điều kiện kiểm tra, nên sĩ số vượt capacity. 