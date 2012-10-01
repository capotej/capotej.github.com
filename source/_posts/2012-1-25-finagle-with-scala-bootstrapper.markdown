---
layout: post
title: "Finagle with scala-bootstrapper"
date: 2012-01-25 09:45
comments: false
permalink: /finagle-with-scala-bootstrapper
categories:
---

 ### Finagle with scala-bootstrapper
January 25 2012,  9:45 AM by Julio Capote

I've been fascinated by the concepts in[finagle](http://twitter.github.com/finagle/)  for some time, but being a scala noob, I never knew how to bootstrap a finagle project. Turns out twitter has a gem, [scala-bootstrapper](https://github.com/twitter/scala-bootstrapper) , that generates a simple thirft based key/value store for you. There's even a[tutorial](http://twitter.github.com/scala_school/searchbird.html)  on how to extend the example project into a distributed search service.

This is a guide on setting it all up locally, it assumes you have Git, Homebrew, and OS X.

1)**Install scala 2.8.1**


123456
$brew versions scala$cd/usr/local/(or wherever you have homebrew installed)$git checkout -b scala281 0e16b9d(make sure the SHA matches versions output)$brew install scala$git checkout master$git branch -D scala281

2)**Install sbt 0.7.4**(assumes you have a ~/bin in your $PATH)


12
$curl -O http://simple-build-tool.googlecode.com/files/sbt-launch-0.7.4.jar > ~/bin/sbt-launch.jar$echo'java -Xmx1G -jar `dirname $0`/sbt-launch.jar "$@"'> ~/bin/sbt

3)**Install scala-bootstrapper**


1
$gem install scala-bootstrapper

4)**Generate finagle project**


12345
$mkdir newbird$cdnewbird$scala-bootstrapper newbird$sbt update$sbttest

5)**Add a Client class**

create newbird/src/main/scala/com/twitter/newbird/Client.scala with


12345678910111213141516171819202122
packagecom.twitter.newbirdimportcom.twitter.finagle.builder.ClientBuilderimportcom.twitter.finagle.thrift.ThriftClientFramedCodecimportcom.twitter.newbird.thrift._importorg.apache.thrift.protocol.TBinaryProtocolimportjava.net.InetSocketAddressclassClient{  valservice=ClientBuilder()    .hosts(Seq(newInetSocketAddress("localhost",9999)))    .codec(ThriftClientFramedCodec())    .hostConnectionLimit(1)    .build()  valclient=newNewbirdServiceClientAdapter(      newthrift.NewbirdService.ServiceToClient(        service,newTBinaryProtocol.Factory))  defget(key:String)=client.get(key)()  defput(key:String,value:String)=client.put(key,value)()}

6)**Running the server**


123
$cdnewbird$sbt> run -f config/development.scala

7)**Playing with the client**


123456
$cdnewbird$sbt consolescala> import com.twitter.newbird.Clientscala> valclient=new Client()scala> client.put("foo","bar")scala> client.get("foo")

**Bonus**

finagle exports a stats url you can curl:


12345678910111213141516171819202122232425262728
$ curl http://localhost:9900/stats.txtcounters:  Newbird/connects: 1  Newbird/requests: 4  Newbird/success: 4gauges:  Newbird/connections: 0  Newbird/pending: 0  jvm_heap_committed: 588251136  jvm_heap_max: 2146828288  jvm_heap_used: 64354560  jvm_nonheap_committed: 83267584  jvm_nonheap_max: 318767104  jvm_nonheap_used: 68655360  jvm_num_cpus: 4  jvm_start_time: 1327511164928  jvm_thread_count: 14  jvm_thread_daemon_count: 9  jvm_thread_peak_count: 14  jvm_uptime: 2626505labels:metrics:  Newbird/connection_duration: (average=2590412, count=1, maximum=2590412, minimum=2590412, p25=2590412, p50=2590412, p75=2590412, p90=2590412, p99=2590412, p999=2590412, p9999=2590412)  Newbird/connection_received_bytes: (average=192, count=1, maximum=192, minimum=192, p25=192, p50=192, p75=192, p90=192, p99=192, p999=192, p9999=192)  Newbird/connection_requests: (average=4, count=1, maximum=4, minimum=4, p25=4, p50=4, p75=4, p90=4, p99=4, p999=4, p9999=4)  Newbird/connection_sent_bytes: (average=120, count=1, maximum=120, minimum=120, p25=120, p50=120, p75=120, p90=120, p99=120, p999=120, p9999=120)  Newbird/request_latency_ms: (average=14, count=4, maximum=39, minimum=2, p25=2, p50=8, p75=10, p90=39, p99=39, p999=39, p9999=39)

 

 