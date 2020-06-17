## Transforms
---

Transform as the name implies transforms the user-provided template. Transforms are powered by a feature in CloudFormation called Macros. 

A Macro is a lambda function which take an user provided template make changes and provide a transformed template.

AWS CloudFormation provides two global macros:

* AWS::Include
* AWS::Serverless

*These macro's are hosted by CloudFormation and not owned by any customer.* Customer's can also define their own custom Macros that can be used to transform templates.

Macro's can be used to transform the entire template or a part of the template.

---

### [AWS::Include](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/create-reusable-transform-function-snippets-and-add-to-your-template-with-aws-include-transform.html)

---

Let's take a look at a simple template that makes use of the `AWS::Include` Macro:

1. Use the template in the repository `instance.yml` to create an EC2 Instance.

**NOTE:** *When using `Transforms` you would need to use the CreateChangeSet Operation in order to view the transformed template*

```bash
CHANGE_SET_ID=$(aws cloudformation create-change-set --stack-name instance --change-set-type CREATE --change-set-name initial --region us-east-1 --template-url https://deepak-content.s3.amazonaws.com/bucket_new.yml --capabilities CAPABILITY_IAM --query Id --output text)
```

Execute the change-set:

```bash
aws cloudformation execute-change-set --change-set-name $CHANGE_SET_ID
```

You can see that the base-template didn't have the user-data content or a Mappings section. But upon transformation the template has these sections.

`AWS::Include` is a simple substitution macro. Next, we are going to explore `AWS::Serverless` a much more complicated transform.