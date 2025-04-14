# Spider

## To view the scan results
curl http://localhost:8081/JSON/ajaxSpider/view/status/?apikey=jmdckddvs34n24ohhosllhn494

## To start the Spider scan (Response: Scan ID). Modify the API Key and URL to suite the target
curl "http://localhost:8081/JSON/ajaxSpider/action/scan/?apikey=jmdckddvs34n24ohhosllhn494&url=http://localhost:8001/WebGoat&inScope=&contextName=&subtreeOnly="

## To view the scan results
curl "http://localhost:8081/JSON/ajaxSpider/view/status/?apikey=jmdckddvs34n24ohhosllhn494"


# Attacking the ap

## To view the number of records left to be scanned
curl "http://localhost:8081/JSON/pscan/view/recordsToScan/?apikey=jmdckddvs34n24ohhosllhn494"

## To view the alerts of passive scan
curl "http://localhost:8081/JSON/core/view/alerts/?apikey=jmdckddvs34n24ohhosllhn494&baseurl=http://localhost:8001&start=0&count=10"

# To start the the active scan
curl "http://localhost:8081/JSON/ascan/action/scan/?apikey=jmdckddvs34n24ohhosllhn494&url=http://localhost:8001&recurse=true&inScopeOnly=&scanPolicyName=&method=&postData=&contextId="

# To view the alerts of active scan
curl "http://localhost:8081/JSON/core/view/alerts/?apikey=jmdckddvs34n24ohhosllhn494&baseurl=http://localhost:8001&start=0&count=10"

# Baseline Scan Works
docker run --network host -t ghcr.io/zaproxy/zaproxy:stable zap-baseline.py -t http://127.0.0.1:8080/WebGoat/

# Full Scan
docker run --network host -t ghcr.io/zaproxy/zaproxy:stable zap-full-scan.py -t http://127.0.0.1:8080/WebGoat/
