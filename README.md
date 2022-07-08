# Grafana - influxdb 설치 및 연동방법

<p>
<img src="https://img.shields.io/badge/InfluxDB-22ADF6?style=flat&logo=InfluxDB&logoColor=white"/>
<img src="https://img.shields.io/badge/Grafana-F46800?style=flat&logo=Grafana&logoColor=white"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=flat&logo=Docker&logoColor=white" alt="Badge"/>

</p>

Grafana 와 influx db를 연동하기
<br>

<br>

## Grafana / influxdb 설치

---

도커 이미지 배포

```
docker network create influxdb
docker run -d --net=influxdb --name=grafana -p 3000:3000 grafana/grafana
docker run -d --net=influxdb --name=influxdb -p 8086:8086 influxdb
```

or 직접 설치

```
# 1. Grafana 설치
# adduser, libfontconfg1 설치

sudo apt-get install -y adduser libfontconfig1

# grafana 다운로드
wget https://dl.grafana.com/oss/release/grafana_7.5.2_amd64.deb
# grafana 설치
sudo dpkg -i grafana_7.5.2_amd64.deb

# 실행
sudo service grafana-server start
sudo service grafana-server status

# 2. influxdb 설치

wget https://dl.influxdata.com/influxdb/releases/influxdb2-2.0.4-amd64.deb
sudo dpkg -i influxdb2-2.0.4-amd64.deb    
sudo service influxdb start
sudo service influxdb status

```

이후 종료하고싶으면 sudo service influxdb stop로 종료한다

## localhost 서버확인

---

설치가 완료되었으면

[http://localhost:3000](http://localhost:3000)

[http://localhost:8086](http://localhost:8086)

로컬호스트에 접속하여 확인해본다

<br>

## influxdb 초기설정

---

0. [http://localhost:8086](http://localhost:8086) 에 접속한다
1. influx db의 id/pw 를 직접 설정해준다
2. Load Data 의 Token 값을 저장한다
3. 프로필 사진 클릭후 About 에서 org id 값을 저장한다
4. 새 버킷을 하나 만든다

## grafana 초기설정

---

0. [http://localhost:3000](http://localhost:3000) 에 접속해 grafnana 의 초기 id/pw 인 admin / admin 으로 접속
1. Configuration/Plugins 에서 TrackMap 인스톨
2. Configuration/Data source에서 Add data source -> influxdb 를 선택해준다
3. Query Language 를 Flux 로 변경
4. HTTP-URL 을 http://localhost:8086 로 변경 단,Docker 사용시 http://influxdb:8086 로 변경한다
5. Organization 입력
6. Token 입력
7. Default Bucket 입력
8. save & test 버튼클릭
9. buckets found 가 뜨면 성공

![](https://lh3.googleusercontent.com/fife/AAWUweU8Lao-dstG4ZW9cHzzTdvtuFK6a2h-y6psd8c6aALajmn9dNXMM-nWsGFpgJbMrLm-mhFlc2q4D2jdZvE5W_iajARaXBr8OCC9xl_XkiLLL-j2b1NclnUSvW8r12lABWJeX-l5DxZVM2YGXI6j0Ro5Ww3E2YuMJZHJVKx28VMi00fUjkHdCouY8A1OHSmUcetEtPx24xTwo6iJW-YCzJNgPWdJ4N4rU9jnrcWJ_PGdY8wH7tqdkXDzTQIOVP2UllBYzcT8kpapKvA4U2e-xtzKY7lXQIwrT22mVXU12X4pgcen72mjc0eIyYtVsa6T3axZn0Lv6IWqMqMZLz5DGItoUh6Ikb1Hr1zrqWSKYlmCKfN52SScQ7ybwjsJhshAxeuTpr_Bvs4EPix0UMX1tjrUKBRuX3x5giQ-A-0sCPNgDisfhbNBTCOKXP_0iTpNxiWFDGxmr_FAjLe38B6yTfuHYVITtRkxOV9eCZPhu07JHYChLYw3RZw43Qp4Jg9X-4ocn71q1AfeqQrA5BogEBfeAo3-iXGcJUDrVe3gATUm4wbA4t4obzXXSBSSjITDOBkoHUap6Qy0gPPBCCqgbHFB0-xFIYTm7Hlf0o8bB4QZJEs1lpPymOMy4aWLyUr6N94_QTkpeAnP0yQQqdpefYh674q6yIWjIUgn_NKZBQD_s1hJyofekqd3veEc9Vz8Sb3010vMFwnml5Czavjrs4F6o5fCAg8gS-r6uvIfMsZqFmvRJ0YWKJq2sFGdl3ka5dJDgkyaGXy21kpVassk7i8epgIwx1sE3cwTM_-5lQ3uxPHnAbF-aVE_l86cLqYjQGtqQsdyTlU0AIxzL4RTGmWZgR0phgQwyFzL1eEuRYBe6wHnJ1IoPBUycHpLRLCCt5iDwcL4jf36XcZ2Jqkx3JUElVC6ZfaeC57xmpw7iPSoLwlGoW47knuw19D3BXjc6edwPPIiqtZ7BV7ZnasY5XSOKkHpWVPmXQhYHRJQVMm1ljRSFm9GW4yqfZ0HqvRf1BudHIgI7xFgijeEaiz6UCzaj5sKPbDaRIbS6m4ZTvR-zyBDP8h2DDQ05mRTY9pm04-DxfrYMstvgBsSB4Rpznzr9NGZeCVj7xKziVF3jQVMAtngjiXKOQ4fytR2sdQkgkXkMQncH4miw0vHIHrxnNxCAKyY8mfQHJTEEzvwnAGgzWOjCUZnKl_LNriVDOVISzVQz0mV60iqbINVBc_NBXRNzD2rqTayj7AU_jjI1uJMB5xn1bKlTAT5nkgk6x-TPBcNLyk=w1920-h942)
