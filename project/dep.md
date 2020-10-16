# Package Dependencies

## Base

* JDK = "14.0.2"

```scala
scalaVersion := "2.13.3"
 
libraryDepedencies ++= Seq(
  "org.scalatest" %% "scalatest" % "3.1.1" % Test
)
```

## Akka gRPC
```scala
lazy val akkaVersion = "2.6.9"
lazy val akkaHttpVersion = "10.2.0"
lazy val akkaGrpcVersion = "1.0.2"

libraryDependencies ++= Seq(
  "com.typesafe.akka" %% "akka-actor-typed" % akkaVersion,
  "com.typesafe.akka" %% "akka-stream" % akkaVersion,
  "com.typesafe.akka" %% "akka-discovery" % akkaVersion,
  "com.typesafe.akka" %% "akka-pki" % akkaVersion,
  // The Akka HTTP overwrites are required because Akka-gRPC depends on 10.1.x
  "com.typesafe.akka" %% "akka-http" % akkaHttpVersion,
  "com.typesafe.akka" %% "akka-http2-support" % akkaHttpVersion,
  "com.typesafe.akka" %% "akka-actor-testkit-typed" % akkaVersion % Test,
  "com.typesafe.akka" %% "akka-stream-testkit" % akkaVersion % Test
}
```

* plugins.sbt
```scala
addSbtPlugin("com.lightbend.akka.grpc" % "sbt-akka-grpc" % "1.0.2")

addSbtPlugin("com.lightbend.sbt" % "sbt-javaagent" % "0.1.5")
```

* Apply SBT Plugin
```scala
  enablePlugins(AkkaGrpcPlugin)
```
