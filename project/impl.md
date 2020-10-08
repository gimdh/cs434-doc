# Implementation Details

## Libraries in Use

* See [Package Dependencies](dep.md) for detailed version information

### [Akka](https://akka.io/)
Entire networking is based on Akka framework. Specifically, below two protocols are used.

* [Akka gRPC](https://github.com/akka/akka-grpc)  with [protobuf](https://developers.google.com/protocol-buffers) for communication.
* [Akka Streaming File IO](https://doc.akka.io/docs/akka/current/stream/stream-io.html#streaming-file-io) for efficient file transfer.

### [Log4j 2 Scala API](https://logging.apache.org/log4j/2.x/manual/scala-api.html)
Defacto standard logging library.

