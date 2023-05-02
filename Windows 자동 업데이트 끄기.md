## Introduction

<br>

- 상시로 켜둬야 하는 PC 프로세스가 재부팅으로 인해 꺼지는 경우가 가끔 있다.
- `Windows update`로 인한 경우가 많은데, 자동 업데이트를 꺼두고 필요할 때마다 업데이트를 하면 이런 사고 아닌 사고를 방지할 수 있다.
- 아래는 `Command prompt`를 이용하여 `Windows update`를 비활성화 하는 방법을 알아본다.

<br>

## Command prompt 명령어 또는 bat 파일 작성

<br>

1. 아래 항목을 Command prompt에 한줄씩 입력한다.
    ```cmd
    sc config "uhssvc" start=disabled
    sc config "wuauserv" start=disabled
    sc config "UsoSvc" start=disabled
    REG ADD HKLM\SYSTEM\CurrentControlSet\Services\WaasMedicSvc /v Start /f /t REG_DWORD /d 4

    sc stop "uhssvc"
    sc stop "wuauserv"
    sc stop "WaasMedicSvc"
    sc stop "UsoSvc"
    ```
2. 해당 명령어를 `*.bat` 파일로 만드려는 경우, 아래와 같이 만들어준다.
    ```bat
    @echo off
    sc config "uhssvc" start=disabled
    sc config "wuauserv" start=disabled
    sc config "UsoSvc" start=disabled
    REG ADD HKLM\SYSTEM\CurrentControlSet\Services\WaasMedicSvc /v Start /f /t REG_DWORD /d 4

    sc stop "uhssvc"
    sc stop "wuauserv"
    sc stop "WaasMedicSvc"
    sc stop "UsoSvc"
    pause
    ```
    - 위의 명령어 중 `@echo off` 및 `pause`는 취향에 따라 넣어준다.
      - `@echo off`는 프롬프트에 입력되는 명령어를 보이지 않게 한다.
      - `pause`는 모든 작업 실행 후 cmd 창이 자동으로 닫히는 것을 방지한다.