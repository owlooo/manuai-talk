# 실행 방법·코드 입구

[개인 기여 요약](../README.md)

## 프런트엔드 실행

Node.js와 npm을 준비한 뒤 저장소 루트에서 실행합니다.

```bash
cd Full/Frontend
npm install
npm run dev
```

이 명령은 프런트엔드 개발 서버만 시작합니다. 채팅·음성·인증 기능에는 백엔드와 해당 서비스 설정이 필요합니다.
`NEXT_PUBLIC_API_URL`, `NEXT_PUBLIC_WS_URL`은 실행 환경의 API·WebSocket 주소로 설정합니다.
키·계정·비밀번호는 개인 환경파일에서 관리합니다.

- [실행 스크립트와 의존성](../Full/Frontend/package.json)
- [백엔드 코드·실행 자료](../Full/Backend)

## 개인 구현의 코드 입구

| 영역 | 파일 |
|---|---|
| 채팅·세션 | [useChat](../Full/Frontend/src/features/chat/hooks/useChat.ts) · [상태 저장소](../Full/Frontend/src/store/useChatStore.ts) |
| 음성 재생 | [TTSPlayer](../Full/Frontend/src/components/chat/TTSPlayer/TTSPlayer.tsx) · [스트림 처리](../Full/Frontend/src/features/chat/utils/tts.ts) |
| QR | [ProductQRCode](../Full/Frontend/src/components/product/ProductQRCode/ProductQRCode.tsx) |
| AR 연동 | [ARUI](../Full/Frontend/src/components/ar/ARUI.tsx) |

## 프로젝트 기록

- 기획 포함 기간: 2025.09.25~12.10. 기업 연계 개발 기간: 2025.10.20~12.10.
- 광주인공지능사관학교 우수상: 2025.12.11.
- 데모 URL은 2026.09.20 확인 시 HTTP 404였습니다. 현재 코드·기여 이력을 중심으로 열람할 수 있습니다.
- [정리 전 팀 문서](https://github.com/TextNest/PandDF_ManuAITalk/blob/9cfa65b41d1b6ee68dcc73bbac9451a217b528b1/README.md)는 개발 당시 기록입니다. 초기 완성도·진행률은 현재 상태를 나타내지 않습니다.
