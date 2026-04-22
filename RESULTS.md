# Results

## 1. 실험 요약
- 저장소: exp-stt-whisper-webgpu
- 커밋 해시: 5e875c5
- 실험 일시: 2026-04-22T06:13:41.781Z -> 2026-04-22T06:13:41.781Z
- 담당자: ai-webgpu-lab
- 실험 유형: `audio`
- 상태: `success`

## 2. 질문
- segment 단위 partial emission과 최종 완료 시간이 안정적으로 측정되는가
- reference transcript 기준 WER/CER가 보고 포맷에 그대로 반영되는가
- 실제 Whisper runtime 연결 전 파일 전사 baseline 경로를 검증할 수 있는가

## 3. 실행 환경
### 브라우저
- 이름: Chrome
- 버전: 147.0.7727.15

### 운영체제
- OS: Linux
- 버전: unknown

### 디바이스
- 장치명: Linux x86_64
- device class: `desktop-high`
- CPU: 16 threads
- 메모리: 16 GB
- 전원 상태: `unknown`

### GPU / 실행 모드
- adapter: not-applicable
- backend: `mixed`
- fallback triggered: `false`
- worker mode: `main`
- cache state: `cold`
- required features: []
- limits snapshot: {}

## 4. 워크로드 정의
- 시나리오 이름: File Transcription
- 입력 프로필: 7.4s-2-segments
- 데이터 크기: deterministic segment fixture; segments=2; transcriptLength=15; automation=playwright-chromium
- dataset: transcript-fixture-v1
- model_id 또는 renderer: -
- 양자화/정밀도: -
- resolution: -
- context_tokens: -
- output_tokens: -

## 5. 측정 지표
### 공통
- time_to_interactive_ms: 176.2 ms
- init_ms: 91.3 ms
- success_rate: 1
- peak_memory_note: 16 GB reported by browser
- error_type: -

### STT
- audio_sec_per_sec: 81.05
- first_partial_ms: 42.3 ms
- final_latency_ms: 91.3 ms
- wer: 0
- cer: 0

## 6. 결과 표
| Run | Scenario | Backend | Cache | Mean | P95 | Notes |
|---|---|---:|---:|---:|---:|---|
| 1 | File Transcription | mixed | cold | 81.05 | 91.3 | first_partial=42.3 ms, WER=0 |

## 7. 관찰
- partial emission은 42.3 ms에 시작됐고 최종 latency는 91.3 ms였다.
- deterministic transcript fixture 기준 WER=0, CER=0가 기록됐다.
- playwright-chromium로 수집된 automation baseline이며 headless=true, browser=Chromium 147.0.7727.15.
- 실제 runtime/model/renderer 교체 전 deterministic harness 결과이므로, 절대 성능보다 보고 경로와 재현성 확인에 우선 의미가 있다.

## 8. 결론
- 파일 전사 baseline의 timing, transcript, error scoring 경로가 실제 결과로 고정됐다.
- 다음 단계는 Whisper runtime과 real audio asset을 연결해 같은 보고 포맷으로 교체하는 것이다.
- partial latency와 final latency를 브라우저/모드별로 반복 측정할 필요가 있다.

## 9. 첨부
- 스크린샷: ./reports/screenshots/01-file-transcription.png
- 로그 파일: ./reports/logs/01-file-transcription.log
- raw json: ./reports/raw/01-file-transcription.json
- 배포 URL: https://ai-webgpu-lab.github.io/exp-stt-whisper-webgpu/
- 관련 이슈/PR: -
