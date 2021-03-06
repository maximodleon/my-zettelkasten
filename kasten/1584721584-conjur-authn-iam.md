# 1584721584 conjur-authn-iam
#conjur #authn

The conjur `authn-iam` authenticator allows the ability to authenticate using an AWS IAM role.


## Advantages
- No secret zero
- Use AWS identities to retrieve secrets from conjur
- IAM roles are widely accepted and understood

## Disadvatages
- Creation of the signed request requires code within the application

## Configuration
```yaml
- !policy
  id: conjur/authn-iam/<service id>
  body:
  - !webservice
  - !group apps
  - !permit
    role: !group apps
    resource: !webservice
    privileges: [ read, authenticate ]

# an example of a host that will authenticate using an IAM role
- !host team1/<aws account number>/<iam role name>
- !grant
  role: !group conjur/authn-iam/<service id>/apps
  member: !host team1/<aws account number>/<iam role name>
```

Once the policy has been loaded we must enable the authenticator by execing into the conjur appliance and performing the following:
```bash
evoke variables set CONJUR_AUTHENTICATORS=authn,authn-iam/<service id>
```

## Use cases
- [Authenticating an AWS Fargate or ECS instance](1585068641-aws-fargate-iam-authn-conjur.md)
- [Authenticating an EC2 instance (python)](https://github.com/AndrewCopeland/conjur-iam-api-key#ec2-usage)
- [Authenticating an EC2 instance (cli)](https://github.com/AndrewCopeland/conjur-authn-iam-client/tree/master/docs/ec2#authenticating-ec2-with-cli)
- [Authenticating a Lambda function (python)](https://github.com/cyberark/conjur-authn-iam-client-python#lambda-usage)
- [Authenticating a Lambda Function (go)](https://github.com/AndrewCopeland/conjur-authn-iam-client/tree/master/docs/lambda)
- [Using summon with IAM role on EC2 (python)](https://github.com/AndrewCopeland/conjur-iam-api-key#summon-usage)
- [Authenticating using Java](https://github.com/AndrewCopeland/conjur-iam-api-key-java/blob/master/src/ConjurApi/AwsIamAuthn/ConjurAwsIamAuthn.java)
- [Authenticating using Powershell](https://github.com/AndrewCopeland/conjur-api-powershell/blob/master/CyberarkConjur.psm1#L286-L314)
- [Authenticating using .NET Core](https://github.com/AndrewCopeland/conjur-api-net-core/blob/master/src/ConjurClient/Authenticators/AuthnIAMHelper.cs)

## Links
- [1585072449-conjur-home-authenticators.md](1585072449-conjur-home-authenticators.md)
- [1585068641-aws-fargate-iam-authn-conjur.md](1585068641-aws-fargate-iam-authn-conjur.md)
- [1585328995-ec2-metadata-url-token.md](1585328995-ec2-metadata-url-token.md)
- [1585603925-lambda-access-key-environment-vars.md](1585603925-lambda-access-key-environment-vars.md)
- [1586469583-aws-eks-iam-roles-with-service-accounts.md](1586469583-aws-eks-iam-roles-with-service-accounts.md)
- [1595942906-aws-lambda-function-python-conjur-example.md](1595942906-aws-lambda-function-python-conjur-example.md)
