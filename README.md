# ci-cd-codedeploy

1. AWS EC2 Instance 생성

2. Instance 태그 추가
   
   <img width="842" alt="Instance 태그 추가" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/f051853e-32ac-42a5-8bd2-09afbbfee20d">

3. 보안 그룹 설정
   
   <img width="1775" alt="보안 그룹 설정" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/c24df349-ae8c-48be-86a8-9601bf831479">

4. EIP 할당
   
   <img width="1594" alt="EIP 할당" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/84f98a26-267d-427f-bac3-a18239d49fda">

5. EC2 Instance에 codedeploy agent 설치
  ```Bash
  # 시스템의 패키지 목록을 업데이트하고 설치된 패키지를 최신 버전으로 업그레이드.
  $ sudo apt update && sudo apt upgrade 
  
  # Ruby 언어의 전체 설치 버전을 시스템에 설치.
  $ sudo apt install ruby-full
  
  # 네트워크를 통해 파일을 다운로드하는 명령어인 wget을 설치.
  $ sudo apt install wget
  $ cd /home/ubuntu
  
  # AWS CodeDeploy 에이전트 설치 스크립트 다운로드.
  $ wget https://aws-codedeploy-ap-northeast-2.s3.ap-northeast-2.amazonaws.com/latest/install
  
  # 다운로드한 설치 스크립트에 실행 권한 부여.
  $ chmod +x ./install
  
  # AWS CodeDeploy 에이전트를 자동으로 설치하고 출력을 로그 파일로 저장.
  $ sudo ./install auto > /tmp/logfile
  
  # AWS CodeDeploy 에이전트의 서비스 상태 확인.
  $ sudo service codedeploy-agent status
  ```
  ![EC2 Instance에 codedeploy agent 설치](https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/79ea6b56-b336-4912-b54a-f209832a111c)

6. Node.js 설치
  ```Bash
  # NVM 설치
  $ curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
  
  # NVM 환경 변수 설정
  $ export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"
  
  $ nvm install 20.5.0
  $ nvm use 20.5.0
  $ node -v
  ```

7. Nest CLI 설치
  ```Bash
  $ npm install -g @nestjs/cli
  $ nest -v
  ```

8. EC2 IAM 역할 생성 및 EC2 연결
   <img width="1129" alt="EC2 IAM 역할 생성 및 EC2 연결1" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/5eb37c39-ecbf-4e63-9c87-b2b6e133df92">
   <img width="1504" alt="EC2 IAM 역할 생성 및 EC2 연결2" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/2136a3eb-8208-47fe-bede-6e911a262bfa">
   <img width="825" alt="EC2 IAM 역할 생성 및 EC2 연결3" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/ea773d39-f3f1-4505-b22c-a12d7305cffa">

9. S3 Bucket 생성
    
   <img width="818" alt="S3 Bucket 생성" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/192c8d31-a9ad-4be7-83f6-8b26b9370121">

10. S3용 IAM 사용자 생성
    
    <img width="1514" alt="S3용 IAM 사용자 생성" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/ee9de832-8096-4889-b111-4fd036305df2">

11. 사용자 → 보안자격 증명 → 액세스 키 → 액세스 키 만들기
    
    <img width="1611" alt="사용자 → 보안자격 증명 → 액세스 키 → 액세스 키 만들기" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/fcc490a2-a62a-48d2-9190-1949848523f0">

12. 액세스 키와 비밀 액세스 키 저장
    
    <img width="1498" alt="액세스 키와 비밀 액세스 키 저장" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/a1b7006c-f8ac-4eaa-b03d-d6837e85d568">

13. CodeDeploy IAM 역할 생성
    
    <img width="1582" alt="CodeDeploy IAM 역할 생성" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/c5c8190e-bfd6-4063-8b5b-ab257997f210">

14. CodeDeploy 애플리케이션 생성
    
    <img width="826" alt="CodeDeploy 애플리케이션 생성" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/3b074407-4242-4282-b775-22e6e488ed11">

15. CodeDeploy 배포 그룹 생성 - 생성한 CodeDeploy IAM 역할 설정 및 환경 구성 EC2 인스턴스 태그 추가
    
    <img width="1543" alt="생성한 CodeDeploy IAM 역할 설정 및 환경 구성 EC2 인스턴스 태그 추가1" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/b8d64330-760b-4cbd-813f-44ec18fcb2d5">
    <img width="824" alt="생성한 CodeDeploy IAM 역할 설정 및 환경 구성 EC2 인스턴스 태그 추가2" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/eee73278-b16d-4568-9426-e00621f6e683">
    <img width="732" alt="생성한 CodeDeploy IAM 역할 설정 및 환경 구성 EC2 인스턴스 태그 추가3" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/b42d86db-c1f3-45e7-b29b-63a5a128412d">

16. Github Repository 생성

17. 배포할 프로젝트 root 경로에 appspec.yml 파일 생성
    ```yml
    version: 0.0
    os: linux
    files:
      - source: /
        destination: /home/ubuntu/github_action
        overwrite: yes
    
    permissions:
      - object: /
        pattern: '**'
        owner: ubuntu
        group: ubuntu
    
    hooks:
      ApplicationStart:
        - location: /src/scripts/deploy.sh
          timeout: 60
          runas: ubuntu
    ```

  - version : appspec.yml 파일의 버전을 의미합니다.
  - os : 배포 대상 운영 체제를 지정합니다.
  - files : 배포할 파일과 위치를 지정합니다.
      - source : 배포할 파일이 위치한 소스 디렉토리 경로입니다.
      - destination : 파일을 배포할 대상 경로입니다.
      - overwrite : 대상 위치에 이미 파일이 있을 경우 덮어쓸지 여부를 결정합니다.
  - permissions : 배포된 파일의 권한을 설정합니다.
      - object : 권한을 설정할 대상을 지정합니다.
      - pattern : 권한을 적용할 파일 패턴을 지정합니다. ‘**’는 모든 파일과 디렉토리에 권한을 적용합니다.
      - owner 및 group : 파일의 소유자와 그룹을 지정합니다.
  - hooks : 배포 생명 주기 동안 실행할 스크립트를 정의합니다.
      - ApplicationStart : 애플리케이션 시작 시 실행할 스크립트입니다.
      - location : 스크립트 파일의 위치를 지정합니다. `/src/scripts/deploy.sh` 는 EC2 인스턴스 내 스크립트 파일 경로입니다.
      - timeout : 스크립트 실행이 완료되기를 기다리는 최대 시간(초)입니다.
      - runas : 스크립트를 실행할 사용자를 지정합니다.

18. deploy.sh 파일 생성
    ```sh
    #!/bin/bash
    PROJECT_NAME="github_action"
    DEPLOY_PATH="/home/ubuntu/$PROJECT_NAME/"
    DEPLOY_LOG_PATH="/home/ubuntu/$PROJECT_NAME/deploy.log"
    DEPLOY_ERR_LOG_PATH="/home/ubuntu/$PROJECT_NAME/deploy_err.log"
    APPLICATION_LOG_PATH="/home/ubuntu/$PROJECT_NAME/application.log"
    
    echo "===== 배포 시작 : $(date +%c) =====" >> $DEPLOY_LOG_PATH
    
    echo "> 현재 동작중인 어플리케이션 pid 체크" >> $DEPLOY_LOG_PATH
    CURRENT_PID=$(pgrep -fl "node.*$PROJECT_NAME" | awk '{print $1}')
    
    if [ -z $CURRENT_PID ]
    then
      echo "> 현재 동작중인 어플리케이션 존재 X" >> $DEPLOY_LOG_PATH
    else
      echo "> 현재 동작중인 어플리케이션 존재 O" >> $DEPLOY_LOG_PATH
      echo "> 현재 동작중인 어플리케이션 강제 종료 진행" >> $DEPLOY_LOG_PATH
      echo "> kill -9 $CURRENT_PID" >> $DEPLOY_LOG_PATH
      kill -9 $CURRENT_PID
    fi
    
    echo "> 애플리케이션 배포" >> $DEPLOY_LOG_PATH
    cd $DEPLOY_PATH
    nohup node dist/main.js >> $APPLICATION_LOG_PATH 2> $DEPLOY_ERR_LOG_PATH &
    
    sleep 3
    
    echo "> 배포 종료 : $(date +%c)" >> $DEPLOY_LOG_PATH
    ```

19. Github Actions Secrets 설정 / 빌드시 동적으로 변수값을 주입하기 위해 OVERRIDE_VALUE 설정
    
    <img width="1126" alt="Github Actions Secrets 설정 : 빌드시 동적으로 변수값을 주입하기 위해 OVERRIDE_VALUE 설정" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/13868a94-ce72-4669-8281-d4943546fc64">

20. Github Repository -> Actions → set up a workflow yourself

21. deploy.yml 파일 작성 → commit
    ```yml
    name: CI-CD

    on:
      push:
        branches:
          - main
      workflow_dispatch:
    
    env:
      S3_BUCKET_NAME: asher-devops-test-bucket
      RESOURCE_PATH: src/config/env/.env
      CODE_DEPLOY_APPLICATION_NAME: devops-test-code-deploy
      CODE_DEPLOY_DEPLOYMENT_GROUP_NAME: devops-test
    
    jobs:
      build:
        runs-on: ubuntu-latest
    
        steps:
          - name: Checkout
            uses: actions/checkout@v2
    
          - name: Set up Node.js
            uses: actions/setup-node@v2
            with:
              node-version: 20.5.0
    
          - name: Create .env file
            run: |
              DIRECTORY_PATH=$(dirname $RESOURCE_PATH)
              mkdir -p $DIRECTORY_PATH
              echo "OVERRIDE_VALUE=${{ secrets.OVERRIDE_VALUE }}" >> $RESOURCE_PATH
    
          - name: Install Dependencies
            run: npm install
    
          - name: Build
            run: npm run build
    
          - name: Make zip file
            run: zip -r ./$GITHUB_SHA.zip dist node_modules package.json src/scripts/deploy.sh appspec.yml
            shell: bash
    
          - name: Configure AWS credentials
            uses: aws-actions/configure-aws-credentials@v1
            with:
              aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
              aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
              aws-region: ${{ secrets.AWS_REGION }}
    
          - name: Upload to S3
            run: aws s3 cp --region ${{ secrets.AWS_REGION }} ./$GITHUB_SHA.zip s3://$S3_BUCKET_NAME/$GITHUB_SHA.zip
    
          - name: Code Deploy
            run: |
              aws deploy create-deployment \
              --deployment-config-name CodeDeployDefault.AllAtOnce \
              --application-name ${{ env.CODE_DEPLOY_APPLICATION_NAME }} \
              --deployment-group-name ${{ env.CODE_DEPLOY_DEPLOYMENT_GROUP_NAME }} \
              --s3-location bucket=$S3_BUCKET_NAME,bundleType=zip,key=$GITHUB_SHA.zip
    ```

  - Checkout : GitHub 저장소의 코드를 체크아웃합니다. 워크플로우가 실행되는 러너에 저장소의 코드를 복제합니다.

  - Set up Node.js : 20.5.0 버전의 Node.js를 설정합니다.
  
  - Create .env file : 지정된 경로에 .env 파일을 생성하고, GitHub Secrets에서 ‘OVERRIDE_VALUE’ 값을 이 파일에 추가합니다.
  
  - Install Dependencies : ‘npm install’ 명령어를 사용하여 프로젝트의 종속성을 설치합니다.
  
  - Build : ‘npm run build’ 명령어를 사용하여 애플리케이션을 빌드합니다.
  
  - Make zip file : 빌드된 ‘dist/’ 디렉토리, ‘node_modules’, ‘package.json’, ‘deploy.sh’, ‘appspec.yml’ 파일을 포함하는 ZIP 파일을 생성합니다.
  
  - Configure AWS credentials : AWS 자격증명을 설정하여 AWS 서비스에 액세스할 수 있도록 합니다.
  
  - Upload to S3 : 생성된 ZIP 파일을 AWS S3 버킷으로 업로드합니다.
  
  - Code Deploy : AWS CodeDeploy를 사용하여 S3에 업로드된 ZIP 파일을 EC2 인스턴스에 배포합니다.

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  
## 동적 변수 주입 테스트 결과

로컬

<img width="244" alt="로컬" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/422c3d45-7ce5-46fd-8246-6cc19c2a1be6">

메인 서버

<img width="341" alt="메인 서버" src="https://github.com/ash991213/ci-cd-codedeploy/assets/99451647/f3cacf6f-9f69-46da-87b3-d43f01e25598">

## 에러

메시지 - ERROR [codedeploy-agent(15693)]: InstanceAgent::Plugins::CodeDeployPlugin::CommandPoller: Missing credentials - please check if this instance was started with an IAM instance profile

문제 확인 경로 - /var/log/aws/codedeploy-agent/codedeploy-agent.log

원인 : EC2에 CodeDeploy 관련 IAM Role이 부여되기 전에 CodeDeploy Agent가 실행되면서 IAM Role을 못 가져간 것

조치 : sudo service codedeploy-agent restart
    
