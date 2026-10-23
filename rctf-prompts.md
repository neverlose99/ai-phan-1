## Prompt 1
**Role:**  
Bạn là lập trình viên PHP Laravel có kinh nghiệm.

**Context:**  
Tôi đang phát triển chức năng đăng nhập cho một ứng dụng quản lý khóa học bằng Laravel. Người dùng đăng nhập bằng username và password. Bảng `accounts` có các cột `id`, `username`, `password`, `status`. Chỉ tài khoản có `status = active` mới được đăng nhập.

**Task:**  
Viết phương thức đăng nhập trong Controller. Kiểm tra dữ liệu đầu vào, xác thực tài khoản và từ chối tài khoản không hoạt động. Không tự viết câu SQL ghép chuỗi. Giải thích ngắn gọn cách hoạt động.

**Format**  
Trả về code PHP có thể tích hợp vào Laravel, kèm giải thích và các trường hợp cần kiểm thử. Không sử dụng dữ liệu tài khoản thật.

**Kết quả**

use Illuminate\Http\Request;
use Illuminate\Support\Facades\Auth;
public function login(Request $request)
{
    $credentials = $request->validate([
        'username' => ['required', 'string'],
        'password' => ['required', 'string'],
    ]);
    $account = \App\Models\Account::where(
        'username',
        $credentials['username']
    )->first();
    if (!$account || $account->status !== 'active') {
        return back()->withErrors([
            'username' => 'Thông tin đăng nhập không hợp lệ.',
        ]);
    }
    if (!\Illuminate\Support\Facades\Hash::check(
        $credentials['password'],
        $account->password
    )) {
        return back()->withErrors([
            'username' => 'Thông tin đăng nhập không hợp lệ.',
        ]);
    }

    Auth::login($account);
## Prompt 2
**Role** Bạn là lập trình viên Backend chuyên tối ưu ứng dụng PHP Laravel và MySQL.

**Context** Trang quản lý khóa học hiển thị danh sách tài khoản và khóa học tương ứng. Mỗi tài khoản có thể tham gia nhiều khóa học thông qua bảng trung gian `account_course`. 

**Task** Phân tích nguyên nhân có thể gây truy vấn N+1 và đề xuất cách tối ưu bằng Eloquent ORM. Giữ nguyên kết quả nghiệp vụ, không thay đổi cấu trúc cơ sở dữ liệu. Giải thích cách kiểm tra hiệu quả sau khi sửa.

**Format** Cung cấp code trước và sau khi tối ưu, giải thích sự khác biệt, kèm 3 bước kiểm tra. Không sử dụng dữ liệu thật của người dùng.
**Kết quả**

Trước khi tối ưu:
$accounts = Account::all();

foreach ($accounts as $account) {
    foreach ($account->courses as $course) {
        echo $course->name;
    }
}


Nếu quan hệ courses chưa được tải trước, vòng lặp có thể phát sinh nhiều truy vấn.

Sau khi tối ưu:
$accounts = Account::with('courses')->get();

foreach ($accounts as $account) {
    foreach ($account->courses as $course) {
        echo $course->name;
    }
}
## Prompt 3
**Role** Bạn là lập trình viên Backend chuyên phát triển ứng dụng bằng PHP Laravel và MySQL.

**Context** Tôi đang phát triển hệ thống quản lý khóa học bằng Laravel. Hệ thống có bảng `accounts` lưu tài khoản người dùng, bảng `courses` lưu thông tin khóa học và bảng trung gian `account_course` lưu quan hệ đăng ký khóa học. Một tài khoản có thể đăng ký nhiều khóa học và một khóa học có thể có nhiều tài khoản tham gia.

**Task** Hãy phát triển chức năng đăng ký khóa học cho người dùng đã đăng nhập. Yêu cầu:
- Kiểm tra người dùng đã đăng nhập.
- Kiểm tra khóa học có tồn tại và còn cho phép đăng ký.
- Không cho phép một tài khoản đăng ký cùng một khóa học nhiều lần.
- Lưu thông tin đăng ký vào bảng `account_course`.
- Trả về thông báo thành công hoặc lỗi phù hợp.
- Sử dụng Eloquent ORM và kiểm tra dữ liệu đầu vào an toàn.

**Format** Cung cấp code Laravel cho Route, Controller và phần xử lý quan hệ Model cần thiết; giải thích từng bước và đưa ra 3 trường hợp kiểm thử. Nếu chưa biết cấu trúc chính xác của dự án, hãy nêu rõ các giả định thay vì tự khẳng định code có thể chạy ngay.
