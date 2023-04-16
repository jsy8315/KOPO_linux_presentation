---
layout: home
---

# 리눅스 시간설정
> https://psychoria.tistory.com/750

## 타임존이란?
타임존(Time Zone)은 지구상의 각 지역에서 사용하는 시간대를 의미합니다. 지구는 자전과 공전으로 인해 자연스럽게 시간이 흐르지만, 각 지역에서는 일정한 시간을 사용해야 하므로 타임존이 필요합니다.

## GMT 기준
세계적으로 24개의 타임존이 있으며, 각 타임존은 GMT(Greenwich Mean Time)을 기준으로 시간 차이를 나타냅니다. 예를 들어, 한국 표준시(KST)는 GMT+9입니다. 즉, 한국은 GMT보다 9시간 빠르게 시간이 흐릅니다.

## UTC
타임존은 일반적으로 UTC(Coordinated Universal Time)를 기준으로 표시됩니다. UTC는 국제표준시로, 원자시계를 기반으로 정확하게 유지되는 시간입니다. 따라서, UTC를 기준으로 타임존의 차이를 계산하면 세계 각 지역의 현재 시각을 확인할 수 있습니다.

## 설정
리눅스 시스템에서는 타임존을 설정하여 지역 시간을 정확하게 유지할 수 있습니다. 대부분의 리눅스 배포판에서는 `/etc/localtime` 파일을 통해 타임존을 설정하며, 타임존 설정은 주로 시스템 설정 시에 수행됩니다. 

## 관련 명령어
리눅스에서 타임존을 확인하기 위해서는 다음과 같은 명령어를 사용할 수 있습니다.

```bash
timedatectl
```
