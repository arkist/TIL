# TIL
Today I learned ¯\_(ツ)_/¯


## Unix Command

* *nohup* - no hang up. 프로세스 백그라운드 실행
    * http://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_nohup_%EC%82%AC%EC%9A%A9%EB%B2%95
    * http://changpd.blogspot.kr/2013/04/linux-nohup-xxxsh.html
* *crontab* - 작업 스케줄러
    * 주기 설정정보 -  `* * * * * script.sh` *은 순서대로 min/hour/day/month/week(0-6,0:sunday)을 의미. 원하는 시간 설정
    * min에 */5 -> 매5분마다 같은식으로도 설정 가능
    * [Jenkins - use of H(hash syntax) in crontab 관련 글](https://issues.jenkins-ci.org/browse/JENKINS-17311) 
    * http://zetawiki.com/wiki/%EB%A6%AC%EB%88%85%EC%8A%A4_%EB%B0%98%EB%B3%B5_%EC%98%88%EC%95%BD%EC%9E%91%EC%97%85_cron,_crond,_crontab


## AngularJS

* config 에는 constants와 provider만 inject 가능
