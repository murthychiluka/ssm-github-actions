```
1 Create the S3 bucket for app packages
 aws s3 mb s3://murthychiluka-deploy-bucket --region us-east-1
2 create role for private server ---AmazonSSMManagedInstanceCore and S3 read access
3. Add S3 + SSM permissions to your GitHubActionsRole in permissions as I have already created OIDC role
4 Get your private server's instance ID
5 Add GitHub repo secrets
  Repo → Settings → Secrets and variables → Actions → New repository secret
Secret name	       Value
AWS_IAM_ROLE	     arn:aws:iam::417521971870:role/GitHubActionsRole
APP_INSTANCE_ID	   The instance ID
S3_DEPLOY_BUCKET	 murthychiluka-deploy-bucket
6. Make sure your repo has an app/ folder

```
The easiest way to remember

Private EC2 + GitHub-hosted runner:     GitHub Actions → S3 → SSM → Private EC2

Private EC2 + self-hosted runner in VPC:  GitHub Actions → Runner → Private EC2
text```

The important takeaway
| Method         | Artifact transfer | Remote command | SSH/22 needed? |
| -------------- | ----------------- | -------------- | -------------- |
| SCP only       | ✅                 | Via SSH        | ✅              |
| SSM + S3       | S3                | SSM            | ❌              |
| SSM + Git pull | GitHub            | SSM            | ❌              |
| SCP + SSM      | SCP               | SSM            | ✅              |


