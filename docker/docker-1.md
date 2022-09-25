# Docker란

도커(Docker)는 리눅스의 응용 프로그램들을 프로세스 격리 기술들을 사용해 컨테이너로 실행하고 관리하는 오픈 소스 프로젝트이다.


# 시행착오 정리 중
- 항상 사용하는 환경 docker file를 목표
- 컨테이너에서는 sudo, nano를 따로 설치해야 함
    - `apt-get update && apt-get install -y sudo`
- Ubuntu OS라고 하더라도, 컨테이너 환경에서는 `systemctl` 명령 실행 안됨
    - container 자체를 다시 시작해야 함
        - `sudo docker restart ContainerId`
- Ubuntu 컨테이너 위에 단순히 mariaDB 설치하는 것이 아닌 docker-compose
