# Ngữ cảnh repository — elasticsearch-analysis-vietnamese

Plugin phân tích tiếng Việt cho Elasticsearch, kết nối Lucene với tokenizer native.

## 1. Trách nhiệm và luồng xử lý

Analyzer/tokenizer/filter được đăng ký qua plugin; Maven đóng gói theo phiên bản Elasticsearch và thư viện native trong môi trường build.

Giữ tương thích Elasticsearch/Lucene/JDK và ABI tokenizer. Kiểm thử dấu tiếng Việt, offset, stopword và token position; thay analyzer có thể cần reindex, không chỉ cập nhật image.

## 2. Điểm bắt đầu trong mã

- [src/main/java](../src/main/java).
- [src/test/java](../src/test/java).
- [pom.xml](../pom.xml).
- [Dockerfile](../Dockerfile).

Đọc hướng dẫn tại thư mục con trước khi sửa module tương ứng. Đối chiếu hợp đồng và nơi gọi khi thay đổi API, dữ liệu hoặc thư viện dùng chung.

## 3. Toolchain và kiểm chứng

Chuẩn bị môi trường theo [Dockerfile](../Dockerfile), [pom.xml](../pom.xml). Phiên bản runtime của image và dependency phát triển cần được đối chiếu khi khác nhau.

| Mục đích | Thư mục chạy | Lệnh | Điều kiện và tác động |
| --- | --- | --- | --- |
| Build/test plugin | `.` | `mvn verify` | JDK/Elasticsearch và tokenizer native theo pom.xml, Dockerfile, workflow test; không tự cài plugin vào cluster. |

Điểm vào bộ kiểm thử: [src/test/java/org/elasticsearch/index/analysis/VietnameseAnalysisIntegrationTests.java](../src/test/java/org/elasticsearch/index/analysis/VietnameseAnalysisIntegrationTests.java), [src/test/java/org/elasticsearch/index/analysis/VietnameseAnalysisTests.java](../src/test/java/org/elasticsearch/index/analysis/VietnameseAnalysisTests.java). Đọc setup/fixture trước khi chạy rộng hơn; những đường dẫn này không biểu thị mức bao phủ của toàn hệ thống.

Ghi kết quả và phạm vi thực sự đã chạy trong PR. Không ghi build, lint hoặc test thành công khi mới đọc cấu hình hay khi script không thực thi assertion.

## 4. Cấu hình và phát hành

Đường tự động hóa được xác định trong các workflow sau. Điều kiện branch/tag/path quyết định lúc chạy; bước phát hành cần được đọc cùng quyền và môi trường của job.

| Workflow | Điều kiện kích hoạt |
| --- | --- |
| [.github/workflows/test.yml](../.github/workflows/test.yml) | push; pull_request |

Cấu hình đóng gói/chạy: [Dockerfile](../Dockerfile).

Dùng credential được cấp cho đúng môi trường. Không lưu secret hoặc dữ liệu cá nhân vào mã, tài liệu, ảnh chụp hay log. Migration, seed, publish, gửi thông báo và rollout là thao tác có tác động; chỉ thực hiện trong phạm vi công việc và môi trường đã được giao. Phiên bản đang phục vụ cần được xác định từ artifact/deployment, không chỉ từ default branch.

## 5. Tiêu chuẩn chung và duy trì

Áp dụng [Engineering Standards](https://github.com/droppii/engineering-knowledge/tree/docs/repository-context-pilot/handbook/standards/standards.md), [Principles](https://github.com/droppii/engineering-knowledge/tree/docs/repository-context-pilot/handbook/principles/principles.md) và [AI Context](https://github.com/droppii/engineering-knowledge/tree/docs/repository-context-pilot/handbook/ai-context/README.md). Cấu trúc đang có giải thích cách tìm mã; những phần chưa theo tiêu chuẩn cần được cải thiện khi sửa, không trở thành ngoại lệ mặc định.

Cập nhật tài liệu này trong cùng thay đổi khi module, toolchain, public contract, pipeline hoặc điều kiện kiểm thử thay đổi. Quyết định đặc thù cần được ghi ở repository; kiến thức và tiêu chuẩn dùng chung được duy trì tại Engineering Knowledge.

## Profile và workspace theo công việc

[Profile thực thi của repository](../.engineering/README.md) cung cấp cấu hình theo module và điểm vào kiểm chứng local. Chọn profile trong workspace của công việc, chuẩn bị đúng toolchain/dependency, rồi ghi kết quả và giới hạn vào hồ sơ. Kiểm cấu hình hoặc cú pháp thành công chưa thay thế unit/integration test.
