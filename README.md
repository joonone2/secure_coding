

## **✅ SonarQube를 이용한 시큐어코딩 진단**

### **1. SonarQube 설치 및 실행 (Docker 사용)**

- **SonarQube 설치**: Docker로 SonarQube 서버 실행
    - **Docker 명령어**:

```
docker pull sonarqube:latest
docker run -d --name sonarqube -p 9000:9000 sonarqube:latest
```

- **SonarQube 대시보드**: http://localhost:9000
- 

### **2. SonarScanner 설치**

- **SonarScanner 설치**: Mac에서 brew install sonar-scanner
- **SonarScanner 확인**:

```
sonar-scanner --version
```

---

### **3. 취약한 코드 클론**

- **OWASP BenchmarkJava 리포지토리 클론**:

```
git clone https://github.com/OWASP-Benchmark/BenchmarkJava.git
cd BenchmarkJava
```

- **sonar-project.properties 파일 수정**:

```
touch sonar-project.properties
```

- 파일 내용:

```
sonar.projectKey=benchmark
sonar.projectName=OWASP Benchmark
sonar.projectVersion=1.0
sonar.sources=src
sonar.java.binaries=target/classes
sonar.host.url=http://localhost:9000
sonar.token=여기에_복사한_토큰값
```

---

### **4. Maven 빌드**

- **Maven 빌드**:

```
brew install maven
mvn clean install
```

- **빌드 결과**: target/ 폴더와 classes/ 생성 확인

### **5. SonarScanner 실행**

- **SonarScanner 실행**:

```
sonar-scanner
```

- **예상 메시지**:

```
ANALYSIS SUCCESSFUL, you can browse http://localhost:9000/dashboard?id=benchmark
```

---

### **6. 결과 확인**

- **SonarQube 대시보드**: http://localhost:9000
- **Projects → benchmark** 클릭
    - **분석 항목**:
        - Vulnerabilities (취약점)
        - Bugs (버그)
        - Security Hotspots (보안 위험요소)
        - Code Smells (코드 냄새)

---

### **7. 과제 제출용 캡처**

- **필요한 항목 캡처**:
    - **Security** (289 Open issues)
    - **Security Hotspots** (694 Open issues)
    - **Bugs** 항목도 캡처 추가 가능
- **제출 포맷**:
    - **진단 도구명**: SonarQube Community Edition 10.x
    - **취약한 소스코드 출처**: OWASP BenchmarkJava ([Link](https://github.com/OWASP-Benchmark/BenchmarkJava))
    - **진단 결과 화면**: SonarQube 대시보드 캡처 (취약점, 보안 위험요소, 버그 등)

---

### **8. 트러블슈팅 및 오류 해결**

- **401 오류**: sonar.login → **sonar.token**으로 변경 (토큰 인증 방식 사용)
- **404 / Timeout 오류**: SonarQube 초기화 중일 수 있음, Docker 컨테이너 재시작 (docker restart sonarqube)

---

### 추후에 재 접속시!!!

## **SonarQube 종료 방법**

1. **SonarQube 컨테이너 중지**:
    - SonarQube 컨테이너를 종료하려면 docker stop 명령어를 사용합니다.

```
docker stop sonarqube
```

1. 
2. **SonarQube 컨테이너 삭제** (필요 시):
    - SonarQube를 완전히 삭제하려면 docker rm 명령어로 컨테이너를 제거할 수 있습니다.

```
docker rm sonarqube
```

1. 이 명령어는 SonarQube 서버가 필요 없다면 사용하세요.
    
    > 만약
    > 
    > 
    > **재시작할 때마다 새로 시작하려면 이 명령어를 사용하지 마세요.**
    > 
2. **Docker Desktop 종료** (선택사항):
    - Docker Desktop 애플리케이션을 종료하려면 그냥 **Docker 아이콘**을 클릭하고 **Quit Docker Desktop**을 선택합니다.

---

## **✅**

## **나중에 SonarQube 다시 시작하기**

### **1. SonarQube Docker 컨테이너 다시 시작**

### **:**

- SonarQube를 다시 실행하려면, **Docker Desktop을 실행한 상태에서** 아래 명령어를 입력합니다.

```
docker start sonarqube
```

이 명령어는 SonarQube 컨테이너를 **중지된 상태에서 시작**하는 명령입니다.

### **2. SonarQube 컨테이너가 없을 경우 다시 실행하기**

### **:**

- SonarQube 컨테이너를 **삭제한 후** 다시 실행하려면, 아래 명령어를 통해 **새로 띄울 수 있습니다**.

```
docker run -d --name sonarqube -p 9000:9000 sonarqube:latest
```

- 그 후 [**http://localhost:9000**](http://localhost:9000/) 에 접속하여 다시 **SonarQube 대시보드**에 접속 가능합니다.

### **3. SonarScanner 분석 재실행**

### **:**

- SonarQube 서버가 돌아가고 있다면, 그 다음에 **SonarScanner**를 실행할 때 sonar-scanner 명령어로 다시 분석을 실행할 수 있습니다.

```
sonar-scanner
```

---

## **✅**

## **추가 팁**

- **컨테이너가 중지된 상태에서도 데이터를 보존**하기 위해 **Docker volumes**를 사용하여 데이터를 저장하는 것이 좋습니다.
- **다시 접속 시** 항상 **SonarQube 대시보드**에서 이전에 진행한 **프로젝트 결과**를 확인할 수 있습니다.

---

## **✅**

## **정리**

- **SonarQube 종료**: docker stop sonarqube
- **다시 시작**: docker start sonarqube 또는 docker run -d --name sonarqube -p 9000:9000 sonarqube:latest
- **SonarScanner 재실행**: sonar-scanner

📌 시큐어코딩 진단도구: SonarQube Community Edition (v10.x)

📌 취약한 소스코드 출처: OWASP BenchmarkJava
https://github.com/OWASP-Benchmark/BenchmarkJava

📌 분석 결과 요약:

- 보안 취약점 (Security): 289건
- 보안 위험 요소 (Security Hotspots): 694건
- 유지보수 이슈: 11k+
- 신뢰성 이슈: 8.2k+

📌 대표적인 취약점 예시:

- 하드코딩된 비밀번호 탐지
- XML 외부 엔티티 접근 차단 필요
- 안전하지 않은 암호화 알고리즘 사용
