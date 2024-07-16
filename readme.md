# Pintos Project – Alarm Clock 개선

<br>
<Br>

## 프로젝트 개요

Pintos 커널의 `timer_sleep()` 함수는 busy waiting 방식으로 구현되어 있어 CPU 자원을 비효율적으로 사용한다. 이를 개선하기 위해 `timer_sleep()` 함수를 busy waiting 없이 동작하도록 수정하는 프로젝트를 수행했다.

<br>
<br>

## 구현 내용

### 1. 개발 환경

- 우분투 가상환경 사용
- 코드 수정 도구: gedit

### 2. 구조체 정의 (thread.h)

- `wakeup_time`: 스레드가 깨어날 시점을 저장
- `sleepelem`: 리스트 요소로 사용

### 3. 정렬 함수

- `wakeup_time`을 기준으로 스레드를 정렬

### 4. 타이머 함수 초기화

- `sleeping_list` 정의 및 초기화

### 5. timer_sleep 함수 수정

- 현재 시간에 `ticks`를 더해 `wakeup_time` 설정
- `sleeping_list`에 정렬 삽입 및 스레드 block 상태로 전환

### 6. timer_interrupt 함수 수정

- `ticks` 증가 시 `sleeping_list` 확인
- `wakeup_time`이 도래한 스레드를 리스트에서 제거하고 깨움

<br>
<br>

## 테스트

- alarm-single
- alarm-multiple
- alarm-simultaneous
- alarm-zero
- alarm-negative

5개의 테스트를 모두 통과하여 기능 개선이 확인되었다.

<br>
<br>

## 결과

개선된 `timer_sleep()` 함수는 busy waiting을 피하고, CPU 자원을 효율적으로 사용하여 시스템 전체 성능을 향상시켰다.
