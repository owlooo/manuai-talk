# ManuAI-talk

제품 매뉴얼을 바탕으로 사용자의 질문에 답하는 AI 상담 서비스입니다.
6인 팀에서 프런트엔드를 주로 맡고 백엔드 개발을 보조했습니다. 제품별 채팅·대화 기록·음성 입출력과 제품 관리·QR·AR 화면을 구현·개선했습니다.

2025.09.25~12.10 · 광주인공지능사관학교 6기

**광주인공지능사관학교 우수상 · 2025.12.11**

## 서비스 시연

<p>
<img src="docs/media/chat-demo.gif" alt="제품에 관한 질문에 답변하고 매뉴얼 이미지를 보여주는 13초 채팅 시연" width="290" />
<img src="docs/media/chat-answer.png" alt="공기청정기 부품 설명과 매뉴얼 이미지가 포함된 답변" width="290" />
</p>

제품별 상담 API에 채팅 화면을 연결해 답변과 매뉴얼 이미지를 표시했습니다.
**13초 채팅 미리보기**와 매뉴얼 이미지가 포함된 답변 화면입니다.

**[QR → 채팅 → AR 시연 영상 파일 · 50초](docs/media/service-demo.mp4)**

2025년 팀 최종 발표 영상에서 발췌했습니다. 제가 맡은 부분은 채팅·음성·제품/QR/AR 화면과 백엔드 연동이며, RAG 상담 기능은 팀에서 함께 만든 결과입니다.

## 제가 맡은 화면과 기능

- **채팅·대화 기록:** 제품별 채팅과 이전 대화 조회 화면을 만들고, WebSocket 응답을 화면에 반영했습니다. 세션·메시지 상태는 Zustand로 관리했습니다. [채팅 Hook](Full/Frontend/src/features/chat/hooks/useChat.ts)
- **음성 입출력:** 녹음한 음성을 STT API로 보내고, 답변을 TTS로 재생하도록 연결했습니다. [음성 재생 코드](Full/Frontend/src/features/chat/utils/tts.ts)
- **제품·QR·AR:** 제품 조회·수정·삭제 화면과 QR 연결을 작업하고, AR 화면에서 해당 제품의 챗봇으로 이동하는 흐름을 개선했습니다. [QR 작업](https://github.com/TextNest/PandDF_ManuAITalk/commit/29dbad86a6e2208bd9bb721cd975af7d42ca7b3e) · [AR 화면](Full/Frontend/src/components/ar/ARUI.tsx)

<details>
<summary>제품 QR과 AR → 챗봇 연결 화면 보기</summary>

<img src="docs/media/product-qr.png" alt="등록한 제품의 상담 화면으로 연결되는 QR 코드" width="740" />

제품 관리 화면에서 제품별 상담 주소를 QR로 제공합니다.

<img src="docs/media/ar-view.png" alt="AR에서 선택한 제품의 챗봇으로 이동하는 제품 목록" width="290" />

AR에서 선택한 제품을 다시 검색하지 않고 해당 제품의 상담으로 이어지도록 연결했습니다.
</details>

## 채팅과 음성 처리 흐름

```mermaid
flowchart LR
    Entry[제품 선택 / QR / AR] --> Chat[제품별 채팅]
    Chat <--> State[대화 기록 / 음성 상태]
    Chat --> API[FastAPI / WebSocket]
    API --> RAG[매뉴얼 기반 상담]
    API --> Reply[텍스트 답변 / TTS 재생]
    Reply --> Chat
```

STT/TTS를 복구할 때 음성 처리 코드와 채팅 상태를 함께 수정했습니다.
재생 시작·종료·오류에 따라 화면 상태가 바뀌도록 TTSPlayer와 상태 저장소를 연결했습니다.

자동 재생이 켜져 있어도 직전 입력이 음성이었을 때만 답변 재생 후 녹음을 다시 시작하도록 했습니다.
재생 컴포넌트가 정리될 때는 WebSocket과 오디오 리소스도 함께 정리하도록 처리했습니다.

[복구 커밋](https://github.com/TextNest/PandDF_ManuAITalk/commit/dd13b0bd1bb44d30f130fde9a56fd77414f138e5) · [TTSPlayer](Full/Frontend/src/components/chat/TTSPlayer/TTSPlayer.tsx)

## 실행과 문서

Next.js · React · TypeScript · Zustand · FastAPI · WebSocket · Three.js

- [실행 안내·코드 위치](docs/portfolio-guide.md) · [화면·영상 출처](docs/media/README.md)
- [프런트엔드](Full/Frontend) · [백엔드](Full/Backend) · [원본 팀 저장소](https://github.com/TextNest/PandDF_ManuAITalk)

기존 공개 데모는 현재 접속되지 않습니다(2026.09.20 확인). 위 영상과 화면은 프로젝트 당시 시연 기록입니다.
