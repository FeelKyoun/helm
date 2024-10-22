#쓴 명령어


keytool -importcert -alias ca -file ca.crt -keystore truststore.p12 -storetype PKCS12 -storepass Qhdks100% -noprompt

kubectl create secret generic zipkin-truststore \
  --from-file=truststore.p12=truststore.p12 \
  --from-literal=truststore-password=Qhdks100% \
  -n elk-stack

  kubectl create secret generic zipkin-truststore \
  --from-file=truststore.p12=truststore.p12 \
  --from-literal=truststore-password=Qhdks100% \
  -n elk-stack




  curl -k -X POST \
  -H "Content-Type: application/json" \
  -d '[
        {
          "traceId": "3",
          "id": "3",
          "name": "test-span",
          "timestamp": 22222222222220,
          "duration": 7000,
          "localEndpoint": {
            "serviceName": "test-service",
            "ipv4": "127.0.0.1"
          },
          "tags": {
            "http.method": "GET",
            "http.path": "/test"
          }
        }
      ]' \
  http://133.186.208.74:31790/api/v2/spans