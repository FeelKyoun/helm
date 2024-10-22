# elasticsearch pod 접속 및 해당 경로에 있는 ca 파일 내용 확인 후 복사
cat /usr/share/elasticsearch/config/certs/ca.crt

# 이후 해당 내용의 ca.crt 파일 생성


# 키스토어 추가 작업 진행 / storepass에 패스워드 입력
keytool -importcert -alias ca -file ca.crt -keystore truststore.p12 -storetype PKCS12 -storepass Qhdks100% -noprompt 

# 해당 파일로 secret 생성
kubectl create secret generic zipkin-truststore \
  --from-file=truststore.p12=truststore.p12 \
  --from-literal=truststore-password=Qhdks100% \
  -n elk-stack

## zipkin test
curl -X POST -H "Content-Type: application/json" -d '[{"traceId":"1","id":"1","name":"test-span","timestamp":1622547800000000,"duration":5000,"localEndpoint":{"serviceName":"test-service","ipv4":"127.0.0.1"},"tags":{"http.method":"GET","http.path":"/test"}}]' http://133.186.208.74:32743/api/v2/spans