# aws-go
A Golang httpclient for interfacing with AWS.

### custom http client based on official aws guide for setting up httpclient

How to use this module

Create a golang file with the following configuration
```go

package main

import (
    "github.com/GaryLouisStewart/aws_go"
    "github.com/aws/aws-sdk-go/aws/session"
    "github.com/aws/aws-sdk-go/service/iam"
    "github.com/aws/aws-sdk-go/aws"
)


 httpClient, err := NewHTTPClientWithSettings(HTTPClientSettings{
    Connect:           5 * time.Second,
    ExpectContinue:    1 * time.Second,
    IdleConn:          60 * time.Second,
    ConnKeepAlive:     20 * time.Second,
    MaxAllIdleConns:   75,
    MaxHostIdleConns:  10,
    ResponseHeader:    5 * time.Second,
    TLSHandshake:      5 * time.Second,
 })

if err, != nil {
    fmt.Println("Got an error creating custom HTTP client:")
    fmt.Prinln(err)
    return
}

sess := session.Must(session.NewSession(&aws.Config{
    HTTPClient: httpClient,
    Region: aws.String("eu-west-2")
}))

svc := iam.New(sess)
```
