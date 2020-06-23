# Intrinsic Functions/Внутренние функции

### Base64
```
{"Fn::Base64:valueToEncode"}
or

!Base64 valueToEncode

```

### FindInMap in Mappings

{"Fn::FindInMap:["MapName", "TopLevelKey", "SecondLevelKey"]}

```
        "ImageId": {
          "Fn::FindInMap": [
            "MainAMI",
            {
              "Ref": "AWS::Region"
            },
            "HVM64"
          ]
        },
```

### Cidr
{"Fn::Cidr":[ipBlock, count, cidrBits]} 

This example create 6 CIDRs with a subnet mask "/27" inside from a CIDR with a mask of "/24".

JSON
{ "Fn::Cidr" : [ "192.168.0.0/24", "6", "5"] }

### GetAtt

"Fn::GetAtt" : [ "myELB" , "DNSName" ]

```
{"Fn::GetAtt" : [ "EC2Main" , "PublicDnsName" ]}
{"Fn::GetAtt" : [ "BastionInstance", "PublicIp" ]}
```

### GetAZs

```
{ "Fn::GetAZs" : "region" }
{ "Fn::GetAZs" : { "Ref" : "AWS::Region" } }

``` 

### ImportValue

{ "Fn::ImportValue" : sharedValueToImport }

{ "Fn::ImportValue" : {"Fn::Sub": "${NetworkStackNameParameter}-SubnetID" } }

### Sub
Встроенная функция Fn :: Sub заменяет переменные во входной строке указанными вами значениями

{ "Fn::Sub": [ "www.${Domain}", { "Domain": {"Ref" : "RootDomainName" }} ]}

### Join

```
    "GenerateRandomPassLambda": {
      "Type": "AWS::Lambda::Function",
      "Properties": {
        "Code": {
          "ZipFile": {
            "Fn::Join": [
              "",
              [
                "import boto3\n",
                "import random\n",
```

### Select

```
{ "Fn::Select" : [ "1", [ "apples", "grapes", "oranges", "mangoes" ] ] }

```

### Split

```
{ "Fn::Split" : [ "|" , "a|b|c" ] }
```

### Transform

```

{
   "Fn::Transform" : {
       "Name" : "AWS::Include",
       "Parameters" : {
           "Location" : {"Fn::FindInMap" : ["RegionMap", "us-east-1", "s3Location"] }
        }
    }


}

```

###  Pseudo (global variables)

AWS::REGION
AWS::AccountId
AWS::NotificationARNs
AWS::NoValue
AWS::Partition
AWS::StackId
AWS::StackName
AWS::URLSuffix

### Conditions
Fn::And
Fn::Equals
Fn::If
Fn::Not
Fn::Or

```
  "Parameters" : {
    "EnvType" : {
      "Description" : "Environment type.",
      "Default" : "test",
      "Type" : "String",
      "AllowedValues" : ["prod", "test"],
      "ConstraintDescription" : "must specify prod or test."
    }
  },
```
  
```
  "Conditions" : {
    "CreateProdResources" : {"Fn::Equals" : [{"Ref" : "EnvType"}, "prod"]}
  },

```



