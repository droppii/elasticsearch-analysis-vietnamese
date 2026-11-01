# Hướng dẫn làm việc — elasticsearch-analysis-vietnamese

## Ngữ cảnh Engineering

Plugin phân tích tiếng Việt cho Elasticsearch, kết nối Lucene với tokenizer native.

Đọc [ngữ cảnh repository](docs/repository-context.md) để chọn đúng module, toolchain, kiểm tra và đường phát hành. Đọc hướng dẫn thư mục con khi đi vào phạm vi tương ứng.

Chuẩn dùng chung: [AI Context](https://github.com/droppii/engineering-knowledge/tree/docs/repository-context-pilot/handbook/ai-context/README.md) và [Standards](https://github.com/droppii/engineering-knowledge/tree/docs/repository-context-pilot/handbook/standards/standards.md). Ghi revision đã dùng và kết quả kiểm chứng trong PR; cập nhật ngữ cảnh cùng mã.

Giữ tương thích Elasticsearch/Lucene/JDK và ABI tokenizer. Kiểm thử dấu tiếng Việt, offset, stopword và token position; thay analyzer có thể cần reindex, không chỉ cập nhật image.

## Profile thực thi

Đọc [.engineering/README.md](.engineering/README.md) để chọn profile theo module và nhu cầu kiểm chứng. Dùng checkout/worktree do công cụ agent quản lý theo công việc; phân biệt kiểm nguồn, kiểm mã và kiểm thử hành vi.
