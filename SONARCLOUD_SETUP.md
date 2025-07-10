# 🔍 SonarCloud Setup Guide

## Tổng quan

Repository này đã được cấu hình sẵn để tích hợp với **SonarCloud** cho việc phân tích chất lượng code tự động. SonarCloud sẽ phân tích:

- **Code Quality**: Bugs, Vulnerabilities, Code Smells
- **Security**: Phát hiện lỗ hổng bảo mật
- **Maintainability**: Đánh giá khả năng bảo trì code
- **ESLint Issues**: Lỗi và cảnh báo từ ESLint

## 📋 Các bước setup

### 1. Tạo tài khoản SonarCloud

1. Truy cập [sonarcloud.io](https://sonarcloud.io)
2. Đăng nhập bằng GitHub account
3. Import repository này vào SonarCloud

### 2. Lấy thông tin cấu hình

Sau khi import project, bạn sẽ có:
- **Organization Key**: `your-organization`
- **Project Key**: `your-organization_your-repository`

### 3. Cập nhật file cấu hình

Sửa file `sonar-project.properties`:

```properties
# Thay đổi các giá trị này
sonar.projectKey=your-actual-organization_your-actual-repository
sonar.organization=your-actual-organization
sonar.projectName=Your Actual Project Name
```

### 4. Setup GitHub Secrets

Trong repository GitHub, thêm secrets:

**Settings > Secrets and variables > Actions**

- `SONAR_TOKEN`: Token từ SonarCloud
  - Lấy từ: SonarCloud > My Account > Security > Generate Tokens

### 5. Lấy SonarCloud Token

1. Vào [SonarCloud](https://sonarcloud.io)
2. Click avatar > **My Account**
3. Tab **Security**
4. **Generate Tokens**
5. Đặt tên: `GitHub Actions`
6. Copy token và thêm vào GitHub Secrets

## 🔧 Workflow đã được cấu hình

File `.github/workflows/sonarcloud.yml` sẽ chạy khi:

- **Push** vào branch `main` hoặc `develop`
- **Pull Request** được tạo hoặc cập nhật

## 📊 Các chỉ số được phân tích

### Code Quality Metrics
- **Bugs**: Lỗi logic trong code
- **Vulnerabilities**: Lỗ hổng bảo mật
- **Code Smells**: Code có thể cải thiện
- **Duplications**: Code trùng lặp

### TypeScript/React Specific
- **ESLint Issues**: Lỗi từ ESLint
- **TypeScript Errors**: Type safety issues
- **React Best Practices**: Anti-patterns

## 🎯 Chạy analysis locally

```bash
# Install dependencies
npm install

# Run linting
npm run lint

# Generate ESLint report
npm run lint:report

# Build project
npm run build
```

## 📈 Viewing Results

Sau khi workflow chạy xong:

1. Vào [SonarCloud Dashboard](https://sonarcloud.io/projects)
2. Chọn project của bạn
3. Xem các metrics và issues

## 🔄 Quality Gates

SonarCloud sẽ kiểm tra:

- **Duplicated Lines** < 3%
- **Maintainability Rating** = A
- **Reliability Rating** = A
- **Security Rating** = A

## 🛠️ Troubleshooting

### Workflow fails với "Unauthorized"
- Kiểm tra `SONAR_TOKEN` trong GitHub Secrets
- Đảm bảo token chưa expired

### "Project not found"
- Kiểm tra `sonar.projectKey` trong `sonar-project.properties`
- Đảm bảo project đã được import vào SonarCloud

### ESLint issues không hiển thị
- Chạy `npm run lint:report` local để kiểm tra
- Đảm bảo file `eslint-report.json` được tạo

## 📚 Resources

- [SonarCloud Documentation](https://docs.sonarcloud.io/)
- [SonarJS Rules](https://rules.sonarsource.com/javascript)
- [GitHub Actions Integration](https://docs.sonarcloud.io/advanced-setup/ci-based-analysis/github-actions-for-sonarcloud/) 