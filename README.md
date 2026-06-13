<!--
이 파일은 sevenpeaksone/vexaMD repo의 README.md로 사용할 콘텐츠입니다.
sevenpeaksone web UI에서 "Add a README" → 아래 내용 그대로 붙여넣기.
이후 변경은 sevenpeaksone repo 측에서 직접 관리해도 되고,
필요하면 본 파일을 source of truth로 두고 양쪽 동기화해도 됩니다.
-->

# Vexa MD — 배포 채널

> 초경량 Markdown 뷰어 / 에디터 — **Vexa MD**의 공식 인스톨러 배포 저장소

이 저장소는 Vexa MD 데스크톱 앱의 **인스톨러 자산**과 **자동 업데이트 매니페스트(`latest.json`)**만 호스팅합니다. 개발 소스 코드는 별도 저장소에서 관리됩니다.

---

## 📥 다운로드

가장 최신 버전은 [**Releases**](../../releases/latest) 페이지에서 받을 수 있습니다.

| 플랫폼 | 파일 | 설치 방식 |
|--------|------|-----------|
| **Windows** | `Vexa.MD_x.y.z_x64-setup.exe` | NSIS 인스톨러 — 실행하여 설치 |
| **macOS (Apple Silicon)** | `Vexa.MD_x.y.z_aarch64.dmg` | DMG 마운트 → Applications 폴더로 드래그 |
| **Linux (Debian/Ubuntu)** | `vexa-md_x.y.z_amd64.deb` | `sudo dpkg -i <파일>` |
| **Linux (기타)** | `vexa-md_x.y.z_amd64.AppImage` | 실행 권한 부여 후 실행 |

`.app.tar.gz`, `.exe.sig`, `.AppImage.sig` 등은 자동 업데이트용 signature 파일이므로 일반 사용자가 직접 받을 필요는 없습니다.

> **Intel Mac 사용자**: 현재 공식 자동 빌드는 Apple Silicon (M1/M2/M3...) 전용입니다. Intel Mac에서 사용하시려면 (1) Apple Silicon용 빌드를 Rosetta 2로 실행하거나, (2) 소스 저장소에서 직접 빌드하시면 됩니다. 향후 Intel 사용자 수요에 따라 빌드 매트릭스를 다시 추가할 수 있습니다.

---

## 🔒 첫 설치 시 보안 경고

현재 빌드는 **코드 서명(Code Signing)이 적용되지 않은 상태**입니다. 다음 안내에 따라 진행해 주세요.

### Windows
- "Windows에서 PC를 보호했습니다"(SmartScreen) 화면이 나오면 **"추가 정보" → "실행"** 클릭.
- 향후 Authenticode 코드 서명 적용 예정.

### macOS
- "확인되지 않은 개발자" 경고 시:
  1. Finder에서 `.app`을 **Ctrl + 클릭** (또는 우클릭) → **열기**
  2. 다이얼로그에서 **열기** 다시 클릭
- 또는 **시스템 설정 → 개인 정보 보호 및 보안** → "확인 안 됨"으로 차단된 앱 옆 **"무시하고 열기"**.

### Linux
- `.AppImage`는 다운로드 후 실행 권한 필요:
  ```bash
  chmod +x Vexa.MD_x.y.z_amd64.AppImage
  ./Vexa.MD_x.y.z_amd64.AppImage
  ```
- `.deb`는 `sudo dpkg -i` 후 `sudo apt -f install`로 의존성 보완.

---

## 🔄 자동 업데이트

Vexa MD는 앱 실행 후 백그라운드로 새 버전을 확인합니다.

- **확인 주기**: 앱 시작 약 3초 후 1회 백그라운드 체크
- **수동 확인**: 메뉴 → 도움말 → "업데이트 확인"
- **검증**: 모든 업데이트는 minisign 비대칭 서명으로 무결성 검증
- **매니페스트 위치**: `https://github.com/sevenpeaksone/vexaMD/releases/latest/download/latest.json`

업데이트를 일시적으로 미루려면 모달에서 **"나중에"**를 선택하면 같은 버전에 대해서는 자동 모달이 더 이상 표시되지 않습니다. 수동 확인은 항상 동작합니다.

---

## 💻 시스템 요구사항

| OS | 최소 |
|----|------|
| Windows | 10 (1809+) / Server 2019+, x64, WebView2 Runtime (대부분 자동 설치됨) |
| macOS | 11 (Big Sur) 이상, Intel 또는 Apple Silicon |
| Linux | glibc 2.31+ (Ubuntu 20.04, Debian 11 이상 권장), `libwebkit2gtk-4.1` |

메모리 100MB 미만, 디스크 50MB 미만으로 동작합니다 (실 사용 vault 크기 제외).

---

## ✨ 주요 기능

- 📄 Markdown (`.md`, `.markdown`) 외 `.txt`, `.log`, `.json`, `.html`, `.js`, `.vmd` 뷰어
- ✏️ 편집 모드 + 분할 모드 (실시간 미리보기 + 커서 동기 스크롤)
- 🎨 라이트/다크 + 6가지 컬러 테마 + 무제한 커스텀 테마
- 🌍 4개 언어 UI: 한국어 / English / 日本語 / 简体中文
- 🔐 **`.vmd` 암호화 포맷**: AES-256-GCM, 사용자 키 관리, 다중 키 지원
- 🖼️ 프레젠테이션 모드 (F5)
- 🧩 플러그인 시스템 (내장 8종 + 사용자 설치)
- 🖨️ 인쇄 최적화 (A4 자동 분할, PDF 내보내기)
- 🔍 전문 검색, 줌 (50%~200%), TOC 사이드바, 상태바

전체 기능 목록은 [소스 저장소의 FEATURES 문서](https://github.com/thewinmaker-fishwater/vexaMd/blob/main/docs/FEATURES.md)를 참고하세요.

---

## 📜 변경 이력

각 버전의 변경 사항은 [Releases](../../releases) 페이지의 릴리스 노트에서 한국어 / English 두 가지로 확인할 수 있습니다.

---

## 🐞 문제 신고 / 제안

- **버그 / 기능 제안**: [소스 저장소 Issues](https://github.com/thewinmaker-fishwater/vexaMd/issues)에 등록해 주세요.
- 본 저장소(sevenpeaksone/vexaMD)는 인스톨러 배포 전용이라 Issues를 비활성화하거나 안내 용도로만 운영합니다.

---

## 🔗 관련 링크

- **소스 저장소 (개발)**: [thewinmaker-fishwater/vexaMd](https://github.com/thewinmaker-fishwater/vexaMd)
- **개발 문서**: [docs/](https://github.com/thewinmaker-fishwater/vexaMd/tree/main/docs)
- **릴리스 가이드**: [docs/release/GUIDE.md](https://github.com/thewinmaker-fishwater/vexaMd/blob/main/docs/release/GUIDE.md)

---

## ⚖️ 라이선스

본 소프트웨어는 **7peaks © 2026** 저작권 하에 배포되며, 인스톨러 사용은 본 저장소의 [LICENSE.md](./LICENSE.md) 파일에 명시된 최종 사용자 라이선스 계약(EULA)을 따릅니다.

요약:
- ✅ 개인·회사 사용 자유
- ❌ 무단 재배포·판매·역공학·변조·상표 도용·위장 배포 금지
- 자동 업데이트는 minisign 서명 검증 후 적용, telemetry 수집 없음
- 본 소프트웨어는 "AS IS" 제공, 보증 없음

전문은 [LICENSE.md](./LICENSE.md) 파일을 반드시 확인해 주세요.

---

## English Summary

This repository hosts the **official installer binaries** and **auto-update manifest (`latest.json`)** for **Vexa MD**, an ultra-lightweight Markdown viewer/editor built with Tauri 2.

- **Download**: see [Releases](../../releases/latest) for installers (Windows `.exe`, macOS `.dmg`, Linux `.deb` / `.AppImage`).
- **Auto-update endpoint**: `https://github.com/sevenpeaksone/vexaMD/releases/latest/download/latest.json` (signed with minisign).
- **Source code / Issues**: [thewinmaker-fishwater/vexaMd](https://github.com/thewinmaker-fishwater/vexaMd).
- **Note**: builds are currently **unsigned**; SmartScreen / Gatekeeper warnings on first launch are expected. Authenticode and Apple Notarization are planned.
