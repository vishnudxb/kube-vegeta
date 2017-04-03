# Kube-vegeta

Vegeta is a versatile HTTP load testing tool built out of need to drill HTTP services with a constant request rate. It can be used both as a command line utility and a library.

You can learn more from [here](https://github.com/tsenart/vegeta)

Here I am using Kubernetes to run the HTTP LOAD TESTS

# Usage

```

$ git clone https://github.com/vishnudxb/kube-vegeta.git && cd kube-vegeta
$ kubectl create -f vegeta.yml

```

# To view the pods

```
$ kubectl get pods

OUTPUT:

NAME                      READY     STATUS    RESTARTS   AGE
vegeta-4080967759-r0vrw   1/1       Running   0          39s

```

# Login to container & run the below command

```

$ kubectl exec vegeta-4080967759-r0vrw  -i -t -- /bin/bash
root@vegeta-4080967759-r0vrw:/go# echo "GET https://google.com/" | vegeta attack -duration=5s -rate=5 -timeout=1m | tee output.bin | vegeta report

```

# The output should be something like below:

```
Requests      [total, rate]            25, 5.21
Duration      [total, attack, wait]    4.868476381s, 4.799999885s, 68.476496ms
Latencies     [mean, 50, 95, 99, max]  92.05596ms, 74.566002ms, 117.887051ms, 204.344415ms, 294.462895ms
Bytes In      [total, mean]            275641, 11025.64
Bytes Out     [total, mean]            0, 0.00
Success       [ratio]                  100.00%
Status Codes  [code:count]             200:25  
Error Set:

```

# If you want the output in the HTML format
```
root@vegeta-4080967759-r0vrw:/go# cat output.bin | vegeta report -reporter=output > output.html

```
# If you want the output in the JSON format

```
root@vegeta-4080967759-r0vrw:/go# cat output.bin | vegeta report -inputs=output.bin -reporter=json > metrics.json

```
