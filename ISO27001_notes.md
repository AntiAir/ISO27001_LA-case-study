ISO27001_LA_案例實作分析:

# ISO/IEC 27001:2022 資訊安全管理系統實務稽核案卷 (Audit Engagement File) v1

本儲存庫為模擬主導稽核員（Lead Auditor）針對 20 人規模 B2B SaaS 企業執行 ISO/IEC 27001:2022 實地稽核之案卷紀錄與查核表單。

## 稽核基準與參考法規
* ISO/IEC 27001:2022 資訊安全管理系統要求
* 個人資料保護法及其施行細則
* 資通安全管理法

## 案卷目錄結構

/01-governance-and-context
  - 01_[組織脈絡與ISMS範疇審查紀錄](組織脈絡與ISMS範疇審查紀錄.md)
  - 02_管理審查會議紀錄與出席簽到審核管理審查會議紀錄與出席簽到審核.md

/02-risk-assessment-audit
  - 01_風險評估程序與算式合規性查核.md
  - 02_適用性聲明書 (SoA) 項目勾稽表.md

/03-audit-working-papers
  - 01_內部稽核計畫與抽樣策略.md
  - 02_附錄 A 控制措施實地查核表 (Checklist).md
  - 03_稽核抽樣與軌跡證據清冊.md

/04-findings-and-reports
  - 01_不符合事項 (NC) 與觀察事項 (OBS) 報告單.md
  - 02_矯正措施計畫 (CAPA) 審查與結案紀錄.md

## 稽核抽樣與證據對照紀錄

ISO 27001:2022 條文 / 控制項 | 稽核驗證重點 | 實地抽樣與核對證據 | 判定結果
--------------------------- | ------------ | ------------------ | --------
Clause 4.3 範疇界定 | 網路邊界與服務範疇是否完整涵蓋 | 網路拓撲圖、AWS VPC 架構圖、資產清冊 | 符合
Clause 6.1.2 風險評估 | 風險鑑別是否包含 CIA 三要素 | 2026 Q1 風險評估清冊、RTP 風險處置計畫 | 符合
A.5.15 存取權限管理 | 離職與異動帳號清理時效 | 抽查近半年 3 名離職人員 HR 紀錄與 AD/AWS 權限刪除 Log | 不符合 (NC)
A.8.12 資料洩漏預防 | 核心 API 與資料庫防護 | Cloudflare WAF 設定檔、S3 Bucket Public Access 設定 | 符合
A.8.15 日誌留存 | 軌跡完整性與防竄改機制 | Linux auditd 設定檔、S3 Glacier Deep Archive 備份紀錄 | 符合

## 稽核實地觀察紀錄 (Auditor's Field Notes)

### 1. 發現事項紀錄 (Finding - A.5.15)
* 案由：抽查 2026 年 3 月離職名單（共 3 人），發現其中 1 名軟體工程師之 VPN 存取權限，於 HR 辦妥離職手續後第 4 天始完成撤銷。
* 條文依據：ISO/IEC 27001:2022 附錄 A.5.15（存取權限管理）。
* 處置：開立次要不符合事項（Minor NC），要求受稽單位限期提出原因分析與矯正措施（CAPA）。

### 2. 技術控制判定 (Audit Judgment - A.8.15)
* 案由：受稽單位未採購 SIEM 系統，每日 syslog 由腳本自動打包加密，拋送至 AWS S3 進行 1 年期歸檔。
* 判定：接受。查驗 S3 Bucket 已啟用 MFA Delete 及 Write Once Read Many (WORM) 政策，已實質滿足 A.8.15 對於「日誌防竄改」與「軌跡留存」之控制要求，無須開立缺失。

## 備註
本儲存庫表單僅供資安稽核演練、資安顧問輔導與內部稽核流程規劃參考。
---
## 參考資料
1. 資通國家安全法 中文版(https://law.moj.gov.tw/LawClass/LawAll.aspx?pcode=A0030297)
2. 資通國家安全法 英文版 (Cyber Security Management Act, https://law.moj.gov.tw/ENG/LawClass/LawAll.aspx?pcode=A0030297)
