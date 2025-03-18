```markdown
# SonarQube 企业版/开发者版部署指南

## 📥 下载地址
### 企业版 (推荐)
- 最新版 10.7.0.96327 (2024-06)  
  `https://binaries.sonarsource.com/CommercialDistribution/sonarqube-enterprise/sonarqube-enterprise-10.7.0.96327.zip`
- 历史版本 10.6.0.92116  
  `https://binaries.sonarsource.com/CommercialDistribution/sonarqube-enterprise/sonarqube-enterprise-10.6.0.92116.zip`

### 社区版
- v10.6 (92116)  
  [官网下载页](https://www.sonarsource.com/products/sonarqube/downloads/)

---

## 🔑 许可证生成
### 配置模板（选择需要的版本）
```text
# Developer 版
Company=Unknown
Digest=NotRequired
Edition=Developer
EditionLabel=Developer
Expiration=2099-01-01
MaxLoc=9223372036854775806
Plugins=abap,cpp,plsql,security,sonarapex,swift,tsql,vbnet,cobol,pli,rpg,vb
Features=*
ServerId=*
Support=false
Type=123123

# Enterprise 版（推荐）
Company=Unknown
...
Edition=Enterprise
EditionLabel=Enterprise
...

# Datacenter 版（暂不支持破解）
...
```

### 生成步骤
1. 复制上述配置块（包含所有换行）
2. 访问 [Base64在线工具](https://tool.chinaz.com/tools/base64.aspx)
3. 将内容粘贴至编码区 ➔ 生成Base64字符串
4. 将生成的字符串保存为 `license.txt`

---

## 🛠️ 部署说明
### 企业版部署
```bash
wget https://binaries.sonarsource.com/.../sonarqube-enterprise-10.7.0.96327.zip
unzip sonarqube-enterprise-*.zip
mv license.txt sonarqube-enterprise-10.7.0.96327/conf/
./bin/linux-x86-64/sonar.sh start
```

### Docker 部署（开发者版）
```dockerfile
FROM sonarqube:9.9.3-developer
COPY license.txt /opt/sonarqube/conf/
```

---

## ⚠️ 注意事项
1. **版本支持**：
   - ✅ 已验证版本：Developer 9.9.3.79813 / Enterprise 10.6+
   - ❌ 数据中心版暂不可破解
   - ❌ 开发者版不支持CI集成

2. **功能对比**：
   | 功能                | 企业版 | 开发者版 |
   |---------------------|--------|----------|
   | 安全漏洞检测        | ✔️     | ❌       |
   | CI/CD 集成          | ✔️     | ❌       |
   | 高级语言支持        | ✔️     | 部分     |

3. **AI增强特性**（10.7+）：
   - AI代码质量保障
   - STIG/CASA安全报告
   - PyTorch/Jupyter支持

---

## 🔍 版本评估
- **推荐企业版**：完整的安全漏洞检测和CI/CD支持
- 开发者版仅建议用于本地测试环境
- 10.7版新增AI CodeFix等先进功能

> 官方文档：https://docs.sonarsource.com/sonarqube/latest/
``` 
