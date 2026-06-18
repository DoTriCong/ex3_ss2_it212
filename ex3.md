# BÀI 3: Đọc hiểu & Dò lỗi qua Prompt (Phát hiện Ảo giác AI - Hallucination)

## Giải thích nguyên lý sinh lỗi ảo giác
AI thường dựa vào dữ liệu huấn luyện và ngữ cảnh trong prompt để suy luận. Khi người dùng đưa vào một phương thức không tồn tại (ví dụ: `StringUtils.hasSpecialCharacters()`), AI có xu hướng "bịa" ra code để phù hợp với yêu cầu, vì nó nhận định rằng phương thức đó có thể hợp lý trong ngữ cảnh. Đây gọi là **hallucination** – AI sinh ra thông tin không có thật. Nguyên nhân là prompt đã định hướng sai lệch, khiến AI không kiểm chứng lại với tài liệu chính thống.

---

## Prompt tối ưu mới
"Hãy viết cho tôi một hàm Java kiểm tra xem chuỗi đầu vào có chứa ký tự đặc biệt hay không. Vui lòng sử dụng các API chính thức của thư viện chuẩn Java (ví dụ: `java.util.regex.Pattern` và `Matcher`) hoặc các phương thức đã được kiểm chứng trong thư viện phổ biến. Đồng thời, hãy giải thích cơ sở sử dụng (dẫn nguồn từ tài liệu Java chính thức hoặc thư viện phổ biến) để chứng minh phương thức đó thực sự tồn tại."

---

## Mã nguồn Java an toàn do AI sinh ra
```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class SpecialCharChecker {

    // Hàm kiểm tra chuỗi có chứa ký tự đặc biệt hay không
    public static boolean hasSpecialCharacters(String input) {
        if (input == null) {
            return false;
        }
        // Regex: [^a-zA-Z0-9] nghĩa là bất kỳ ký tự nào không phải chữ hoặc số
        Pattern pattern = Pattern.compile("[^a-zA-Z0-9]");
        Matcher matcher = pattern.matcher(input);
        return matcher.find();
    }

    public static void main(String[] args) {
        System.out.println(hasSpecialCharacters("Hello123")); // false
        System.out.println(hasSpecialCharacters("Hello@123")); // true
    }
}
