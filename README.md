# Project to reproduce couldn't import spark.connect proto

This repo is quite simple, just define a simple my.proto where we're going to use
Relation importing from "spark/connect/relations.proto"

```protobuf
syntax = 'proto3';

// Must set the package into spark.connect if importing spark/connect/relations.proto
package spark.connect;

import "spark/connect/relations.proto";

option java_multiple_files = true;
option java_package = "com.example.ml.proto";
//option java_package = "org.apache.spark.connect.proto";
option java_generate_equals_and_hash = true;

message CrossValidatorRelation {
  // (Required) Unique id of the ML operator
  string uid = 1;
  Relation dataset = 2;
}
```

```shell
mvn clean package
```

The above command is going to compile the project, but it's going to throw the exception as follows

```console
[INFO] compiling 1 Scala source and 3 Java sources to spark-connect-proto/target/classes ...
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/CrossValidatorRelation.java:138:39:  error: incompatible types: Relation cannot be converted to MessageLite
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/CrossValidatorRelation.java:154:41:  error: incompatible types: Relation cannot be converted to MessageLite
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/CrossValidatorRelation.java:436:19:  error: no suitable method found for readMessage(org.apache.spark.connect.proto.Relation.Builder,ExtensionRegistryLite)
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/CrossValidatorRelation.java:553:38:  error: type argument Relation is not within bounds of type-variable MType
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/CrossValidatorRelation.java:659:38:  error: type argument Relation is not within bounds of type-variable MType
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/CrossValidatorRelation.java:663:42:  error: type argument Relation is not within bounds of type-variable MType
[ERROR] spark-connect-proto/target/generated-sources/com/example/ml/proto/Relations.java:51:64:  error: incompatible types: org.sparkproject.connect.protobuf.Descriptors.FileDescriptor cannot be converted to com.google.protobuf.Descriptors.FileDescriptor
```
