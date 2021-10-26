# Amazon Comprehend Medical and interface VPC endpoints \(AWS PrivateLink\)<a name="comprehendmedical-vpcendpoints"></a>

You can establish a private connection between your VPC and Amazon Comprehend Medical by creating an *interface VPC endpoint*\. Interface VPC endpoints are powered by [AWS PrivateLink](http://aws.amazon.com/privatelink), a technology that you can use to privately access Amazon Comprehend Medical APIs without an internet gateway, NAT device, VPN connection, or AWS Direct Connect connection\. Instances in your VPC don't need public IP addresses to communicate with Amazon Comprehend Medical APIs\. Traffic between your VPC and Amazon Comprehend Medical does not leave the Amazon network\. 

Each interface endpoint is represented by one or more [Elastic Network Interfaces](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-eni.html) in your subnets\. 

For more information, see [Interface VPC endpoints \(AWS PrivateLink\)](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html) in the *Amazon VPC User Guide*\. 

## Considerations for Amazon Comprehend Medical VPC endpoints<a name="vpc-endpoint-considerations"></a>

Before you set up an interface VPC endpoint for Amazon Comprehend Medical, ensure that you review [Interface endpoint properties and limitations](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#vpce-interface-limitations) in the *Amazon VPC User Guide*\. 

Amazon Comprehend Medical supports making calls to all of its API actions from your VPC\. 

## Creating an interface VPC endpoint for Amazon Comprehend Medical<a name="vpc-endpoint-create"></a>

You can create a VPC endpoint for the Amazon Comprehend Medical service using either the Amazon VPC console or the AWS Command Line Interface \(AWS CLI\)\. For more information, see [Creating an interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#create-interface-endpoint) in the *Amazon VPC User Guide*\.

Create a VPC endpoint for Amazon Comprehend Medical using the following service name: 
+ com\.amazonaws\.*region*\.comprehendmedical

If you turn on private DNS for the endpoint, you can make API requests to Amazon Comprehend Medical using its default DNS name for the Region\. For example, `comprehendmedical.us-east-1.amazonaws.com`\. 

For more information, see [Accessing a service through an interface endpoint](https://docs.aws.amazon.com/vpc/latest/userguide/vpce-interface.html#access-service-though-endpoint) in the *Amazon VPC User Guide*\.

## Creating a VPC endpoint policy for Amazon Comprehend Medical<a name="vpc-endpoint-policy"></a>

You can attach an endpoint policy to your VPC endpoint that controls access to Amazon Comprehend Medical\. The policy specifies the following information:
+ The principal that can perform actions\.
+ The actions that can be performed\.
+ The resources on which actions can be performed\.

For more information, see [Controlling access to services with VPC endpoints](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-access.html) in the *Amazon VPC User Guide*\. 

**Example: VPC endpoint policy for Amazon Comprehend Medical actions**  
The following is an example of an endpoint policy for Amazon Comprehend Medical\. When attached to an endpoint, this policy grants access to the Amazon Comprehend Medical `DetectEntitiesV2` action for all principals on all resources\.

```
{
   "Statement":[
      {
         "Principal":"*",
         "Effect":"Allow",
         "Action":[
            "comprehendmedical:DetectEntitiesV2"
         ],
         "Resource":"*"
      }
   ]
}
```